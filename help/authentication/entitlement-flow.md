---
title: Programmerarens tillståndsflöde
description: Programmerarens tillståndsflöde
exl-id: b1c8623a-55da-4b7b-9827-73a9fe90ebac
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---

# Programmerarens tillståndsflöde {#prog-entitlement-flow}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Ökning {#overview}

Det här dokumentet beskriver det grundläggande tillståndsflödet från programmerarens perspektiv.  Mer information om funktioner och användningsområden utöver den grundläggande TVE-integreringen som beskrivs här finns i [Användningsexempel för programmerare](/help/authentication/programmer-use-cases.md).

Adobe Primetime-autentisering underlättar tillståndsflödet mellan programmerare och distributörer genom att tillhandahålla säkra, enhetliga gränssnitt för båda parter.  På programmerarens sida har Primetime-autentisering två typer av tillståndsgränssnitt:

1. AccessEnabler - En klientkomponent som tillhandahåller ett bibliotek med API:er för appar på enheter som kan återge webbsidor (t.ex. webbappar, smartphone-/surfplatteappar).
2. Klientlöst API - RESTful web services for devices that cannot render web pages (t.ex. set-top boxes, game consoles, smart TV). Kravet på att återge webbsidor bygger på MVPD:s krav på att användarna ska autentisera sig på MVPD:s webbplats.

Förutom den plattformsneutrala översikt som presenteras här finns det en klientlös API-specifik översikt här: API-dokumentation utan klient. AccessEnabler kan köras direkt på plattformar som stöds (AS/JS på webben, Objective-C på iOS och Java på Android). API:erna för AccessEnabler är konsekventa på de plattformar som stöds. Alla plattformar som inte stöder AccessEnabler använder samma klientlösa API.

För båda gränssnittstyperna medierar Primetime-autentisering på ett säkert sätt tillståndsflödet mellan programmerarens app och användarens MVPD:

![](assets/prog-entitlement-flow.png)


*Bild: Adobe Primetime-ekosystem för autentisering*

>[!IMPORTANT]
>
>Observera i diagrammet ovan att det finns en del av tillståndsflödet som inte går via Adobe Primetime autentiseringsservrar: MVPD-inloggningen. Användarna måste logga in på MVPD:s inloggningssida. På enheter som inte kan återge webbsidor måste programmerarens app därför instruera användare att växla till en webbkompatibel enhet för att logga in med sitt MVPD-program, varefter de återgår till den ursprungliga enheten under resten av tillståndsflödet.

## Tillståndsflöde {#entitlement-flow}

Det finns fyra olika delflöden som utgör det grundläggande tillståndsflödet:

1. [Startflöde](/help/authentication/entitlement-flow.md#startup)
1. [Autentiseringsflöde](/help/authentication/entitlement-flow.md#authentication)
1. [Auktoriseringsflöde](/help/authentication/entitlement-flow.md#authorization)
1. [Logout FLow](/help/authentication/entitlement-flow.md#logout)

På en användares första besök på en programmerares webbplats fortsätter tillståndsflödet i den ordning som anges ovan. Vid efterföljande besök, beroende på om autentiserings- och auktoriseringstoken har upphört att gälla eller inte, eller beroende på visningsprofiler, kan en användare bara gå igenom ett eller två av delflödena.

### Startflöde {#startup}

Fastställer programmerarens och enhetens identitet, utför initieringsuppgifter. Detta är en förutsättning för alla efterföljande berättigandeanrop.

**AccessEnabler**

* **`setRequestor()`** - Fastställer din identitet med AccessEnalber, och i tillägg, Adobe Primetime autentiseringsservrar. Anropet är en föregångare till resten av berättigandeflödet. I JavaScript:

  ```JavaScript
    /* Define the requestor ID (Programmer/aggregator ID). */
      var requestorID = "sample_requestor_Id";
      ...
      // Callback indicating that the AccessEnabler swf has initialized
      function swfLoaded() {
          // AccessEnabler is loaded so we can use the API function it provides
          accessEnablerObject.setRequestor(requestorID); 
      ...
      }
  ```

**Klientlöst API**

* **`\<REGGIE\_FQDN\>/reggie/v1/{requestorId}/regcode`** - Beroende på plattformen kan det finnas nödvändiga uppgifter att slutföra innan appanropen kodas om. Se **API-dokumentation utan klient** för mer information. Xbox-plattformarna kräver till exempel att du slutför de föreskrivna säkerhetsstegen innan du anropar regcode.

### Autentiseringsflöde {#authentication}

En AuthN-token som är kopplad till enheten och den som gjorde begäran genereras. Lyckad autentisering är en förutsättning för auktorisering.

**AccessEnabler**

* `checkAuthentication()` - Kontrollerar om det finns en giltig cachelagrad autentiseringstoken i den lokala tokencachen, utan att det fullständiga autentiseringsflödet faktiskt aktiveras. Detta utlöser `setAuthenticationStatus()` callback-funktion.
* `getAuthentication()` - Initierar det fullständiga autentiseringsflödet. Om det lyckas genererar Adobe Primetime-autentiseringen en AuthN-token och cachelagrar den på klienten. Användaren loggar in på sin valda MVPD-webbplats, som visas antingen iFrame, Popup-fönster eller en webbvy, beroende på plattform. Detta utlöser displayProviderDialog().

**Klientlöst API**

* `<FQDN>/.../checkauthn` - webbtjänstversionen av `checkAuthentication()` ovan.
* `<FQDN>/.../config` - Returnerar listan över MVPD-filer till andra skärmappen.
* `<FQDN>/.../authenticate` - Initierar autentiseringsflödet från det andra skärmprogrammet och dirigerar om användare till deras valda MVPD för inloggning. Om det lyckas genererar Adobe Primetime-autentiseringen en AuthN-token och lagrar den på servern, och användaren återgår till sin ursprungliga enhet för att slutföra tillståndsflödet.

En AuthN-token betraktas som giltig om följande två punkter är sanna:

* AuthN-token har inte gått ut
* Det MVPD som är associerat med AuthN-token finns i listan över tillåtna MVPD-filer för aktuellt begärande-ID

#### Allmänt arbetsflöde för inledande autentisering av AccessEnabler {#generic-ae-initial-authn-flow}

1. Ditt program initierar autentiseringsarbetsflödet med ett anrop till `getAuthentication()`som söker efter en giltig cachelagrad autentiseringstoken. Den här metoden har ett valfritt värde `redirectURL` parameter; om du inte anger något värde för `redirectURL`efter en lyckad autentisering returneras användaren till den URL som autentiseringen initierades från.
1. AccessEnabler avgör aktuell autentiseringsstatus. Om användaren är autentiserad anropar AccessEnabler `setAuthenticationStatus()` callback-funktion, skicka en autentiseringsstatus som indikerar att det lyckades.
1. Om användaren inte är autentiserad fortsätter AccessEnabler autentiseringsflödet genom att fastställa om användarens senaste autentiseringsförsök lyckades med ett visst MVPD. Om ett MVPD ID cachelagras OCH `canAuthenticate` flaggan är true ELLER så har ett MVPD valts med `setSelectedProvider()`visas inte dialogrutan för MVPD-val. Autentiseringsflödet fortsätter med det cachelagrade värdet för MVPD (det vill säga samma MVPD som användes vid den senaste autentiseringen). Ett nätverksanrop görs till serverdelen och användaren omdirigeras till inloggningssidan för MVPD.

1. Om inget MVPD ID cachelagras OCH inget MVPD valdes med `setSelectedProvider()` ELLER `canAuthenticate` flaggan är inställd på false, `displayProviderDialog()` återanrop anropas. Det här återanropet dirigerar programmet till det användargränssnitt som visar användaren en lista över MVPD som du kan välja mellan. En array med MVPD-objekt tillhandahålls, som innehåller den information som krävs för att du ska kunna skapa MVPD-väljaren. Varje MVPD-objekt beskriver en MVPD-enhet och innehåller information som MVPD-filens ID och den URL där MVPD-logotypen finns.

1. När ett MVPD-program har valts måste ditt program informera AccessEnabler om användarens val. För klienter som inte är Flashar informerar du AccessEnabler om användarvalet via ett anrop till `setSelectedProvider()` -metod. Flash-klienter skickar i stället en delad `MVPDEvent` av typen &quot;`mvpdSelection`&quot;, skickar den markerade providern.

1. När AccessEnabler informeras om användarens MVPD-val görs ett nätverksanrop till serverdelen och användaren dirigeras om till inloggningssidan för MVPD.

1. I autentiseringsarbetsflödet kommunicerar AccessEnabler med Adobe Primetime-autentisering och det valda MVPD för att begära användarens inloggningsuppgifter (användar-ID och lösenord) och verifiera användarens identitet. Vissa MVPD-program dirigerar om till sin egen webbplats för inloggning, medan andra kräver att du visar deras inloggningssida i en iFrame. Sidan måste innehålla det återanrop som skapar en iFrame om kunden väljer något av dessa MVPD.<!-- For more information on creating a login iFrame, see  [Managing the Login IFrame](https://tve.helpdocsonline.com/managing-the-login-iframe)-->.

1. När användaren har loggat in hämtar AccessEnabler autentiseringstoken och informerar din app om att autentiseringsflödet är slutfört. AccessEnabler anropar `setAuthenticationStatus()` återanrop med statuskoden 1, vilket anger att det lyckades. Om det uppstår ett fel under körningen av dessa steg `setAuthenticationStatus()` callback-funktionen aktiveras med statuskoden 0, vilket anger att autentiseringsfel samt en motsvarande felkod har uppstått.

>[!IMPORTANT]
>Comcast är den enda MVPD-filen för tillfället som inte tillhandahåller en statisk URL för logotypen. Programmerarna bör hämta de senaste logotyperna från [XFINITY Developer&#39;s portal](https://developers.xfinity.com/products/tv-everywhere).
>

### Auktoriseringsflöde {#authorization}

Behörighet krävs för att visa skyddat innehåll. Auktoriseringen genererar en AuthZ-token tillsammans med en kort Media Token som tillhandahålls till programmerarens app av säkerhetsskäl. Observera, att för att stödja auktoriseringsarbetsflödet måste du tidigare ha utfört den begärda konfigurationen och ha integrerat [Media Token Verifier](/help/authentication/media-token-verifier-int.md). När dessa är klara kan du initiera auktoriseringen.

Ditt program initierar auktorisering när en användare begär åtkomst till en skyddad resurs. Du skickar ett resurs-ID som anger den begärda resursen (till exempel en kanal, ett avsnitt osv.). Ditt program söker först efter en lagrad autentiseringstoken. Om det inte går att hitta någon initierar du autentiseringsprocessen.

**AccessEnabler**

* `checkAuthorization()` - Kontrollerar auktoriseringen utan att initiera det fullständiga auktoriseringsflödet. Detta används ofta för att uppdatera statusinformation som visas i programmeringsappens användargränssnitt.

* `getAuthorization()` - Initierar det fullständiga auktoriseringsflödet.

Du tillhandahåller följande återanropsfunktioner för att hantera resultatet av auktoriseringsanropet:

* `setToken()` - Om autentiseringen lyckades tidigare anropar AccessEnabler `setToken()` callback-funktionen, skickar den kortlivade medietoken, vilket anger att Adobe Primetime autentiseringsberättigande har slutförts. (Innan användaren tillåts visa skyddat innehåll kontrollerar programmerarens app giltigheten för medietoken med medietokenverifieraren.

* `tokenRequestFailed()` - Om användaren inte är auktoriserad för den begärda resursen (eller om frågan misslyckas av någon annan anledning) anropar AccessEnabler den här callback-funktionen (plus dina egna felrapporteringsfunktioner) och skickar information om felet.

**Klientlöst API**

* `\<FQDN\>/.../authorize` - Initierar det fullständiga auktoriseringsflödet.

#### Allmänt arbetsflöde för åtkomstaktivering {#generic-ae-authr-wf}

1. Ange en återanropsfunktion som registrerar ditt tilldelade programmerings-GUID med Access Enabler, med `setReqestor()`. Den här återanropsfunktionen anropas när AccessEnabler har hämtats.

1. Utlysning `getAuthorization()` när en användare begär åtkomst till en skyddad resurs. Använda `getAuthorization()`skickar du ett resurs-ID som anger den begärda resursen (till exempel en kanal, ett avsnitt osv.). AccessEnabler söker efter en cachelagrad autentiseringstoken som ska skickas med auktoriseringsbegäran. Om det inte går att hitta någon initierar den autentiseringsflödet.
1. Tillhandahåll återanropsfunktioner för att hantera resultatet av auktoriseringen:

   * `setToken()` - Om auktoriseringen lyckas eller om användaren tidigare har auktoriserats fortsätter åtkomstaktiveringen genom att ringa `setToken()` callback-funktionen, skickar den kortlivade åtkomsttoken.

   * `tokenRequestFailed()` - Om användaren inte är auktoriserad för den begärda resursen (eller om frågan misslyckas av någon annan anledning) anropar AccessEnabler de felrapporteringsfunktioner som du har registrerat, plus `tokenRequestFailed()` återanrop, skickar information om felet.

### Utloggningsflöde {#logout}

Rensar tokens och andra data som är kopplade till den aktuella användarens tillståndsflöde.

**AccessEnabler**

* `logout()`

**Klientlöst API**

* `\<FQDN\>/.../logout`

## Förstå AccessEnabler-beteendet {#ae-behavior}

Alla API-anrop för AccessEnabler är asynkrona (med ett undantag som anges i API-referenserna). Du kan anropa ett API ett godtyckligt antal gånger, men det finns ingen stark garanti för att de åtgärder som utlöses av anropen kommer att slutföras i samma ordning som samtalen gjordes. (Ett undantag till detta är den aktuella Flashens Player körningsmiljö. Om den inte är flertrådig ser den till att anrop utförs *do* i den ordning de anropas.)

För att kunna skilja på svaren och kunna koppla ihop svaren med anrop, återställer alla återanrop sina indataparametrar. Detta inkluderar `setToken()` och`tokenRequestFailed()`, som till slut aktiveras av `checkAuthorization()`. (för `checkAuthorization()` återanrop, resursen som används återställs.) Genom att utnyttja den här funktionen kan du se vilket svar som motsvarar vilket samtal. Om du vill använda den här funktionen kan du koda något av följande:

```JavaScript
    for each (resource in ["TNT", "CNN", "TBS", "AdultSwim"] ) {
         ae.checkAuthorization(resource);
    }
    
    // Success callback
    function setToken(resource, token) {
         // Use "resource" to figure 
         // out which checkAuthorization
         // call triggered this response
    }
    
    // Old error callback
    function tokenRequestFailed(resource, error, details) {
         // use "resource" to figure
         // out in response to which
         // checkAuthorization call
         // this was triggered
    }
    
    // Error callback using new error api
    ae.bind("errorEvent',"errorHandler");
    
    function errorHandler(error) {
         if(error.resource) {        
              // Use error.resource to figure
              // which checkAuthorization call
              // triggered this response
         }
    }
```

### Vanliga frågor om AE-beteende {#ae-beh-faq}

**Fråga. Vad händer om jag gör ett andra AccessEnabler-anrop innan det första anropet avslutas?**

Det första anropet fortsätter att köras när det andra anropet körs (asynkron kommunikation).

**Fråga. Finns det ett maximalt antal samtidiga anrop som AccessEnabler kan stödja?**

Ingen gräns anges uttryckligen i AccessEnabler-koden, så du begränsas bara av dina tillgängliga systemresurser och av MVPD:s kapacitet.

<!--

>[!MORELIKETHIS]
>
>*   [Programmer use cases](/help/authentication/programmer-use-cases.md)
>*   Error Reporting
>**Platform Cookbooks:**
>*   Clientless integration cookbook
>*   iOS Integration Cookbook
>*   Android Integration Cookbook
>*   JavaScript Integration Cookbook
>*   ActionScript Integration Cookbook
>*   Windows 8 Integration Cookbook
>*   AIR Native Extension Overview
-->
