---
title: Android SDK Cookbook
description: Android SDK Cookbook
exl-id: 7f66ab92-f52c-4dae-8016-c93464dd5254
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# Android SDK Cookbook {#android-sdk-cookbook}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

</br>

## Introduktion {#intro}

I det här dokumentet beskrivs de tillståndsarbetsflöden som kan implementeras av ett program på den översta nivån i en programmerare via de API:er som exponeras av Android AccessEnabler-biblioteket.


Adobe Primetime behörighetslösning för autentisering för Android är uppdelad i två domäner:

- Användargränssnittets domän - det här är det övre programlagret som implementerar användargränssnittet och använder tjänsterna som tillhandahålls av AccessEnabler-biblioteket för att ge åtkomst till begränsat innehåll.
- Domänen AccessEnabler - det är här som berättigandearbetsflödena implementeras i form av:
   - Nätverksanrop gjorda till Adobe serverdel
   - Affärslogik för arbetsflödena för autentisering och auktorisering
   - Hantering av olika resurser och bearbetning av arbetsflödestillstånd (t.ex. tokencache)

Målet med AccessEnabler-domänen är att dölja alla komplexa berättigandearbetsflöden och ge programmet i det övre lagret (via AccessEnabler-biblioteket) en uppsättning enkla berättigandeprinciper som du använder för berättigandearbetsflöden:

1. Ange identitet för begärande
1. Kontrollera och hämta autentisering mot en viss identitetsleverantör
1. Kontrollera och få behörighet för en viss resurs
1. Utloggning

Nätverksaktiviteten för AccessEnabler sker i en annan tråd så att gränssnittstråden aldrig blockeras. Det innebär att den tvåvägskommunikationskanal som finns mellan de två programdomänerna måste följa ett fullständigt asynkront mönster:

- Gränssnittets programlager skickar meddelanden till AccessEnabler-domänen via API-anropen som visas av AccessEnabler-biblioteket.
- AccessEnabler svarar på UI-lagret via callback-metoderna i protokollet AccessEnabler som UI-lagret registreras med AccessEnabler-biblioteket.

## Tillståndsflöden {#entitlement}

1. [Förutsättningar](#prereqs)
1. [Startflöde](#startup_flow)
1. [Autentiseringsflöde](#authn_flow)
1. [Auktoriseringsflöde](#authz_flow)
1. [Visa medieflöde](#media_flow)
1. [Utloggningsflöde](#logout_flow)

 

### S. Förutsättningar {#prereqs}

1. Skapa callback-funktioner:
   - [`setRequestorComplete()`](#$setRequestorComplete)

      Utlöses av `setRequestor()`, returnerar om åtgärden lyckades eller misslyckades.  \
      Slutfört visar att du kan fortsätta med berättigandeanrop.

   - [displayProviderDialog(mvpds)](#$displayProviderDialog)

      Utlöses av `getAuthentication()` endast om användaren inte har valt en leverantör (MVPD) och ännu inte är autentiserad.  \
      The `mvpds` är en array med providers som är tillgängliga för användaren.

   - [`setAuthenticationStatus(status, felkod)`](#$setAuthNStatus)

      Utlöses av `checkAuthentication()` varje gång.\
      Utlöses av `getAuthentication()` endast om användaren redan är autentiserad och har valt en leverantör.

      Status som returneras är lyckad eller misslyckad. Felkoden beskriver typen av fel.

   - [navigateToUrl(url)](#$navigateToUrl)

      Utlöses av `getAuthentication()` efter att användaren har valt ett MVPD. The `url` parameter anger platsen för MVPD:s inloggningssida.

   - [`sendTrackingData(event, data)`](#$sendTrackingData)

      Utlöses av `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.\
      The `event` parameter anger vilken tillståndshändelse som inträffat, den `data` parameter är en lista med värden som relaterar till händelsen. 

   - [`setToken(token, resource)`](#$setToken)

      Utlöses av `checkAuthorization()` och `getAuthorization()` efter en auktorisering för att visa en resurs.\
      The `token` parametern är den kortlivade medietoken, den `resource` -parametern är det innehåll som användaren har behörighet att visa.

   - [`tokenRequestFailed(resource, code, description)`](#$tokenRequestFailed)

      Utlöses av `checkAuthorization()` och `getAuthorization()` efter en misslyckad auktorisering.\
      The `resource` parameter är det innehåll som användaren försöker visa, den `code` parameter är felkoden som anger vilken typ av fel som inträffat, den `description` -parametern beskriver felet som är associerat med felkoden.

   - [`selectedProvider(mvpd)`](#$selectedProvider)

      Utlöses av `getSelectedProvider()`.\
      The `mvpd` -parametern ger information om den leverantör som användaren har valt.

   - [`setMetadataStatus(metadata, nyckel, argument)`](#$setMetadataStatus)

      Utlöses av `getMetadata().`\
      The `metadata` parametern innehåller de specifika data som du har begärt, den `key` parametern är nyckeln som används i `getMetadata()` Begäran. och `arguments` parametern är samma ordlista som skickas till `getMetadata()`.

   - [&quot;preauthorizedResources(resources)`](#$preauthResources)

      Utlöses av `checkPreauthorizedResources()`.\
      The `authorizedResources` -parametern visar de resurser som användaren har behörighet att visa.\
       

![](assets/android-entitlement-flows.png)\
 

### B. Startflöde {#startup_flow}

1. Starta programmet på den översta nivån.
1. Initiera Adobe Primetime-autentisering

   a. Utlysning [`getInstance`](#$getInstance) för att skapa en enda instans av Adobe Primetime authentication AccessEnabler.

   - **Beroende:** Inbyggt Android-bibliotek för Adobe Primetime-autentisering (AccessEnabler)

   b. Utlysning` setRequestor()` fastställa programmerarens identitet, skicka in programmerarens `requestorID` och (valfritt) en array med slutpunkter för Adobe Primetime-autentisering.

   - **Beroende:** Giltigt begärande-ID för Adobe Primetime-autentisering\
      (Samarbeta med kontohanteraren för Adobe Primetime-autentisering för att ordna detta.)

   - **Utlösare:** setRequestorComplete(), återanrop

   | ANMÄRKNING |  |
   | --- | --- |  
   | ![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/icons/1313859077_lightbulb.png) | Inga berättigandebegäranden kan slutföras förrän identiteten för den som gjorde begäran har etablerats fullständigt. Detta innebär att när setRequestor() fortfarande körs, kommer alla efterföljande berättigandebegäranden (till exempel `checkAuthentication()`) är blockerade.<br><br>Det finns två implementeringsalternativ: När identifieringsinformationen för den som gjorde begäran skickas till backend-servern kan gränssnittets programlager välja en av följande två metoder:<br><br>1.  Vänta på att utlösaren för `setRequestorComplete()` callback (ingår i AccessEnabler-delegaten).  Det här alternativet ger den största säkerheten för att `setRequestor()` slutförd, så det rekommenderas för de flesta implementeringar.<br>2.  Fortsätt utan att vänta på att utlösaren för `setRequestorComplete()` återanrop och börja utfärda tillståndsansökningar. Dessa anrop (checkAuthentication, checkAuthorization, getAuthentication, getAuthorization, checkPreauthorizedResource, getMetadata, logout) köas av AccessEnabler-biblioteket, som gör att de faktiska nätverksanropen görs efter `setRequestor(). `Det här alternativet kan ibland avbrytas om nätverksanslutningen till exempel är instabil. |

1. Utlysning [checkAuthentication()](#$checkAuthN) för att kontrollera om det finns en befintlig autentisering utan att initiera det fullständiga autentiseringsflödet.   Om samtalet lyckas kan du gå direkt till auktoriseringsflödet.  Om inte, fortsätter du till autentiseringsflödet.

   - **Beroende:** Ett samtal till `setRequestor()` (detta beroende gäller även för alla efterföljande anrop).

   - **Utlösare:** setAuthenticationStatus(), återanrop

 

### C. Autentiseringsflöde {#authn_flow}

1. Utlysning [`getAuthentication()`](#$getAuthN) för att initiera autentiseringsflödet eller för att få en bekräftelse på att användaren redan är autentiserad. \
   **Utlösare:**  
   - Callback-funktionen setAuthenticationStatus(), om användaren redan är autentiserad.  I det här fallet går du direkt till [Auktoriseringsflöde](#authz_flow).
   - Callback-funktionen displayProviderDialog(), om användaren inte har autentiserats ännu.  

1. Visa användaren listan med leverantörer som skickats till `displayProviderDialog()`.

1. När användaren har valt en leverantör hämtar du URL:en för användarens MVPD från `navigateToUrl()` återanrop.  Öppna en WebView och dirigera WebView-kontrollen till URL:en.   

1. Via den WebView-vy som skapades i föregående steg, loggar användaren in på MVPD:s inloggningssida och inloggningsuppgifter. Flera omdirigeringsåtgärder utförs i WebView.\
    

   **Obs!** Nu har användaren möjlighet att avbryta autentiseringsflödet. Om detta inträffar ansvarar ditt UI-lager för att informera AccessEnabler om den här händelsen genom att anropa `setSelectedProvider()` med `null` som en parameter. Detta gör att AccessEnabler kan rensa upp dess interna tillstånd och återställa autentiseringsflödet.

1. När användaren har loggat in identifierar programlagret inläsningen av en &quot;anpassad omdirigerings-URL&quot; (d.v.s.: [http://adobepass.android.app](http://adobepass.android.app/)). Den här anpassade URL:en är en ogiltig URL som inte ska läsas in av WebView. Det är en signal om att autentiseringsflödet har slutförts och att WebView måste stängas.

1. Stäng WebView-kontrollen och anropa `getAuthenticationToken()`, som instruerar AccessEnabler att hämta autentiseringstoken från backend-servern. 

1. [Valfritt] Utlysning [`checkPreauthorizedResources(resources)`](#$checkPreauth) för att kontrollera vilka resurser användaren har behörighet att visa. The `resources` parametern är en array med skyddade resurser som är associerad med användarens autentiseringstoken.\
   **Utlösare:** `preAuthorizedResources()` callback\
   **Körningspunkt:** Efter det slutförda autentiseringsflödet

1. Om autentiseringen lyckades fortsätter du till auktoriseringsflödet.

 

### D. Auktoriseringsflöde {#authz_flow}

1. Utlysning [getAuthorization()](#$getAuthZ) för att initiera auktoriseringsflödet.

   Beroende: Giltiga resurs-ID:n som avtalats med MVPD:n.

   **Obs!** Resurs-ID:n ska vara samma som de som används på andra enheter eller plattformar och ska vara samma för alla programmeringsgränssnitten.

1. Validera autentisering och auktorisering.

   - Om `getAuthorization()` anropet lyckades: Användaren har giltiga AuthN- och AuthZ-tokens (användaren är autentiserad och har behörighet att titta på det begärda mediet).
   - If `getAuthorization()` misslyckas: Undersök undantaget som utlöses för att avgöra dess typ (AuthN, AuthZ eller något annat):
      - Om det var ett autentiseringsfel (AuthN) startar du om autentiseringsflödet.
      - Om det var ett auktoriseringsfel (AuthZ) har användaren inte behörighet att titta på det begärda mediet och någon typ av felmeddelande ska visas för användaren.
      - Om det finns någon annan typ av fel (anslutningsfel, nätverksfel osv.) visar sedan ett felmeddelande för användaren.

1. Validera den korta medietoken.\
   Använd Adobe Primetime Authentication Media Token Verifier-biblioteket för att verifiera den kortlivade medietoken som returneras från `getAuthorization()` ring ovan:

   - Om valideringen lyckas: Spela upp det begärda mediet för användaren.
   - Om valideringen misslyckas: AuthZ-token var ogiltig, mediebegäran ska avvisas och ett felmeddelande ska visas för användaren.

1. Återgå till det normala programflödet.

### E. Visa medieflöde {#media_flow}

1. Användaren väljer de media som ska visas.
2.  Är mediet skyddat?  Programmet kontrollerar om det valda mediet är skyddat:
   - Om det valda mediet är skyddat startar programmet [Auktoriseringsflöde](#authz_flow) ovan.
   - Om det valda mediet inte är skyddat kan du spela upp mediet för användaren.

 

### F. Utloggningsflöde {#logout_flow}

1. Utlysning [`logout()`](#$logout) för att logga ut användaren. \
   AccessEnabler rensar bort alla cachelagrade värden och token för det aktuella MVPD för den aktuella begäraren och även för beställare med enkel inloggning. När cacheminnet har rensats gör AccessEnabler ett serveranrop för att rensa sessionerna på serversidan.  Observera, att eftersom serveranropet kan resultera i en SAML-omdirigering till IdP (detta tillåter sessionsrensning på IdP-sidan), måste det här anropet följa alla omdirigeringar. Därför måste anropet hanteras i en WebView-kontroll.

   a. På samma sätt som autentiseringsarbetsflödet gör AccessEnabler-domänen en en begäran till gränssnittets programlager (via`navigateToUrl()` återanrop) för att skapa en WebView-kontroll och instruera den kontrollen att läsa in URL:en för utloggningsslutpunkten på serverdelen.

   b. Återigen måste gränssnittet övervaka WebView-kontrollens aktivitet och upptäcka när kontrollen, när den går igenom flera omdirigeringar, läser in programmets anpassade URL (d.v.s.: [http://adobepass.android.app/](http://adobepass.android.app/)). När den här händelsen inträffar stänger gränssnittets programlager WebView och utloggningsprocessen är klar.

   **Obs!** Utloggningsflödet skiljer sig från autentiseringsflödet på så sätt att användaren inte behöver interagera med WebView på något sätt. Gränssnittets programlager använder en WebView för att se till att alla omdirigeringar följs. Det är därför möjligt (och rekommenderas) att göra WebView-kontrollen osynlig (dvs. dold) under utloggningsprocessen.

 

### Användarflöden för inloggning med flera MVPD och Logout {#user_flows}

[Här](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AndroidSSOUserFlows.pdf) du har ett dokument som beskriver beteendet när du använder flera PDF-filer och vad som händer när användaren loggar ut från ett program.

Det beskrivna beteendet är tillgängligt när du använder Android SDK version >= 2.0.0.
