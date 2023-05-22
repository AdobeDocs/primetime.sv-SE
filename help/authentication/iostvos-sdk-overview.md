---
title: iOS/tvOS SDK - översikt
description: iOS/tvOS SDK - översikt
exl-id: b02a6234-d763-46c0-bc69-9cfd65917a19
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '3691'
ht-degree: 0%

---

# iOS/tvOS SDK - översikt {#iostvos-sdk-overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.


</br>


## Introduktion {#intro}

iOS AccessEnabler är ett målinriktat iOS/tvOS-bibliotek som gör det möjligt för mobilappar att använda Adobe Primetime-autentisering för TV Everywhere-berättigandetjänster. Implementeringen består av *AccessEnabler* gränssnittet som definierar berättigande-API:t och *EntitlementDelegate* och *[EntitlementStatus](#ios%20entitlement%20status)* protokoll som beskriver återanropen som biblioteket utlöser. Gränssnittet tillsammans med protokollet refereras under ett gemensamt namn: biblioteket AccessEnabler.

## Krav för iOS och tvOS {#reqs}

Aktuella tekniska krav för iOS och tvOS-plattformen och Primetime-autentisering finns i [Plattform/enhet/verktygskrav](#ios)och läsa versionsinformationen som ingår i SDK-nedladdningen. Under resten av den här sidan ser du avsnitt som innehåller ändringar som gäller vissa SDK-versioner och senare. Följande är till exempel en giltig anmärkning om 1.7.5 SDK:

## Understanding Native Client Workflows {#flows}

Inbyggda klientarbetsflöden är vanligtvis desamma som eller mycket lika dem för webbläsarbaserade Primetime-autentiseringsklienter. Det finns dock några undantag, som beskrivs nedan.

- [Arbetsflöde efter initiering](#post-init)
- [Allmänt inledande autentiseringsarbetsflöde](#generic)
- [Utloggningsarbetsflöde](#logout)


### Arbetsflöde efter initiering {#post-init}

Alla tillståndsarbetsflöden som stöds av AccessEnabler förutsätter att du tidigare har anropat [`setRequestor()`](#setReq) för att fastställa din identitet. Du gör det här anropet för att bara ange ditt begärande-ID en gång, vanligtvis under programmets initierings-/installationsfas.


Med en iOS-klient efter första anropet till [`setRequestor()`](#setReq)kan du välja hur du vill fortsätta:

- Du kan börja ringa berättigandesamtal direkt och låta dem stå i kö om det behövs.

- Du kan få en bekräftelse på om [`setRequestor()`](#setReq) genom att implementera [`setRequestorComplete()`](#setReqComplete) återanrop.

- Du kan göra båda av det ovanstående.

Du kan antingen låta din app vänta på ett meddelande om att [`setRequestor()`](#setReq) eller förlita dig på att AccessEnablers anropskömekanism används. Eftersom alla efterföljande autentiserings- och autentiseringsbegäranden behöver begärande-ID och associerad konfigurationsinformation kan [`setRequestor()`](#setReq) metoden blockerar effektivt alla API-anrop för autentisering och auktorisering tills initieringen är slutförd.

 

### Allmänt inledande autentiseringsarbetsflöde {#generic}

Syftet med det här arbetsflödet är att logga in en användare med sitt MVPD. När inloggningen är klar utfärdar backend-servern en autentiseringstoken till användaren. Autentisering sker vanligtvis som en del av auktoriseringsprocessen, men följande beskriver hur autentisering kan fungera fristående och inkluderar inga auktoriseringssteg.

Observera att även om det här arbetsflödet skiljer sig åt för inbyggda klienter från det vanliga webbläsarbaserade autentiseringsarbetsflödet, är steg 1-5 samma för både inbyggda klienter och webbläsarbaserade klienter.

1. Ditt program initierar autentiseringsarbetsflödet med ett anrop till AccessEnabler `getAuthentication() `API-metod som söker efter en giltig cachelagrad autentiseringstoken.
1. Om användaren är autentiserad anropar AccessEnabler [`setAuthenticationStatus()`](#setAuthNStatus) callback-funktion, skicka en autentiseringsstatus som anger att det lyckades och att flödet avslutades.
1. Om användaren inte är autentiserad för tillfället fortsätter AccessEnabler autentiseringsflödet genom att avgöra om användarens senaste autentiseringsförsök lyckades med ett givet MVPD. Om ett MVPD ID cachelagras OCH `canAuthenticate` flaggan är true ELLER så har ett MVPD valts med [`setSelectedProvider()`](#setSelProv)visas inte dialogrutan för MVPD-val. Autentiseringsflödet fortsätter med det cachelagrade värdet för MVPD (det vill säga samma MVPD som användes vid den senaste autentiseringen). Ett nätverksanrop görs till serverdelen och användaren omdirigeras till inloggningssidan för MVPD (steg 6 nedan).
1. Om inget MVPD ID cachelagras OCH inget MVPD valdes med [`setSelectedProvider()`](#setSelProv) ELLER `canAuthenticate` flaggan är inställd på false, [`displayProviderDialog()`](#dispProvDialog) callback anropas. Det här återanropet instruerar programmet att skapa användargränssnittet som visar användaren en lista över MVPD som du kan välja mellan. En array med MVPD-objekt tillhandahålls, som innehåller den information som krävs för att du ska kunna skapa MVPD-väljaren. Varje MVPD-objekt beskriver en MVPD-enhet och innehåller information om exempelvis MVPD-filens ID (t.ex. XFINITY, AT\&amp;T) och den URL där MVPD-logotypen finns.
1. När ett visst MVPD har valts måste programmet informera AccessEnabler om användarens val. När användaren har valt önskat MVPD informerar du AccessEnabler om vilket användarval användaren har via ett anrop till [`setSelectedProvider()`](#setSelProv) -metod.
1. iOS AccessEnabler anropar `navigateToUrl:` callback eller `navigateToUrl:useSVC:` återanrop som dirigerar om användaren till inloggningssidan för MVPD. Genom att aktivera någon av dem skickar AccessEnabler en begäran till ditt program om att skapa en `UIWebView/WKWebView or SFSafariViewController` och läsa in URL:en som finns i callback-funktionen `url` parameter. Detta är URL:en för autentiseringsslutpunkten på backend-servern. För tvOS AccessEnabler är [status()](#status_callback_implementation) callback anropas med `statusDictionary` -parametern och avsökningen för den andra skärmautentiseringen startas omedelbart. The `statusDictionary` innehåller `registration code` som måste användas för den andra skärmautentiseringen. 
1. Om iOS AccessEnabler används, anges inloggningssidan för MVPD som inloggningsinformation via ditt program `UIWebView/WKWebView or SFSafariViewController `styrenhet. Observera att flera omdirigeringsåtgärder utförs under den här överföringen och att programmet måste övervaka de URL:er som läses in av kontrollenheten under de flera omdirigeringsåtgärderna.
1. Om iOS AccessEnabler används `UIWebView/WKWebView or SFSafariViewController` Kontrollenheten läser in en anpassad URL som programmet måste stänga kontrollenheten och anropa AccessEnabler-funktionen `handleExternalURL:url `API-metod. Observera att den här anpassade URL:en är ogiltig och inte avsedd för att styrenheten ska läsa in den. Det får endast tolkas av programmet som en signal om att autentiseringsflödet har slutförts och att det är säkert att stänga `UIWebView/WKWebView or SFSafariViewController` styrenhet. Om ditt program måste använda en `SFSafariViewController `styrenhet som den specifika anpassade URL:en definieras av `application's custom scheme` (t.ex.: `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), annars definieras den här anpassade URL:en av `ADOBEPASS_REDIRECT_URL` konstant (dvs. `adobepass://ios.app`).
1. När programmet stängt `UIWebView/WKWebView or SFSafariViewController` och anropar AccessEnabler `handleExternalURL:url `API-metoden hämtar AccessEnabler autentiseringstoken från backend-servern och informerar programmet om att autentiseringsflödet är slutfört. AccessEnabler anropar [`setAuthenticationStatus()`](#setAuthNStatus) återanrop med statuskoden 1, vilket anger att det lyckades. Om det uppstår ett fel under körningen av dessa steg [`setAuthenticationStatus()`](#setAuthNStatus) callback-funktionen aktiveras med statuskoden 0, vilket anger att autentiseringsfel samt en motsvarande felkod har uppstått.


>[!WARNING]
>
> Under de steg där AccessEnabler släpper kontrollen till ditt program (t.ex. när dialogrutan för val av leverantör visas eller när UIWebView/WKWebView eller SFSafariViewController visas) har användaren möjlighet att avbryta autentiseringsflödet. I dessa situationer ansvarar din app för att informera AccessEnabler om den här händelsen och anropa [`setSelectedProvider()`](#setSelProv) API-metod, skicka null som parameter. Detta ger AccessEnabler en möjlighet att rensa upp det interna tillståndet och återställa autentiseringsflödet. På tvOS kan du använda samma metod för att avbryta autentiseringsavsökningen.


### Utloggningsarbetsflöde {#logout}

För inbyggda klienter hanteras utloggningen på liknande sätt som autentiseringsprocessen som beskrivs ovan.

1. Programmet initierar utloggningsarbetsflödet med ett anrop till AccessEnabler `logout() `API-metod. Utloggningen är resultatet av en serie HTTP-omdirigeringsåtgärder på grund av att användaren måste loggas ut både från Primetime Authentication-servrar och från MVPD-servrarna. Eftersom det här flödet inte kan slutföras med en enkel HTTP-begäran som utfärdas av AccessEnabler-biblioteket är en `UIWebView/WKWebView or SFSafariViewController` styrenheten måste instansieras för att kunna följa HTTP-omdirigeringsåtgärderna.

1. Ett mönster som liknar autentiseringsflödet används. iOS AccessEnabler utlöser `navigateToUrl:` callback eller `navigateToUrl:useSVC:` för att skapa en `UIWebView/WKWebView or SFSafariViewController` och läsa in URL:en som finns i callback-funktionen `url` parameter. Det här är URL:en för utloggningsslutpunkten på backend-servern. För tvOS AccessEnabler finns varken `navigateToUrl:` callback eller `navigateToUrl:useSVC:` callback anropas.

1. När programmet går igenom flera omdirigeringar måste det övervaka aktiviteten i `UIWebView/WKWebView or SFSafariViewController `och identifiera tidpunkten då en viss anpassad URL läses in. Observera att den här anpassade URL:en är ogiltig och inte avsedd för att styrenheten ska läsa in den. Det får endast tolkas av programmet som en signal på att utloggningsflödet har slutförts och att det är säkert att stänga kontrollenheten. När kontrollenheten läser in den här anpassade URL:en måste programmet stänga kontrollenheten och anropa AccessEnabler&#39;s `handleExternalURL:url `API-metod. Om ditt program måste använda en `SFSafariViewController `styrenhet som den specifika anpassade URL:en definieras av `application's custom scheme` (t.ex.`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`), annars definieras den här anpassade URL:en av ` ADOBEPASS_REDIRECT_URL  `konstant (dvs. `adobepass://ios.app`).

1. I slutet av AccessEnabler anropar du [`setAuthenticationStatus()`](#setAuthNStatus) återanrop med statuskoden 0, vilket anger att utloggningsflödet lyckades.

Utloggningsflödet skiljer sig från autentiseringsflödet eftersom användaren inte behöver interagera med `UIWebView/WKWebView or SFSafariViewController`  på något sätt. Därför rekommenderar Adobe att du gör kontrollen osynlig (dvs. dold) under utloggningsprocessen.

## Tokens {#tokens}

- [Definitioner och användning](#definitions)
- [Riktlinjer för cachelagring](#caching)
- [Persistence](#persistence)
- [Format](#format)
- [Enhetsbindning](#device_binding)


### Definitioner och användning {#definitions}

Primetimes behörighetslösning för autentisering gäller generering av specifika datadelar (tokens) som genereras av Primetime-autentisering när autentiserings- och auktoriseringsarbetsflödena har slutförts. Dessa token lagras lokalt på klientens iOS-enhet.

 

Tokens har begränsad livslängd. När tokens upphör att gälla måste de utfärdas på nytt genom att autentiserings- och/eller auktoriseringsarbetsflödena återupptas.

 

Det finns tre typer av tokens som utfärdas under tillståndsarbetsflödena:

- **Autentiseringstoken:** Slutresultatet av användarautentiseringsarbetsflödet blir ett autentiserings-GUID som AccessEnabler kan använda för att göra auktoriseringsfrågor för användarens räkning. Detta autentiserings-GUID har ett associerat TTL-värde (time-to-live) som kan skilja sig från användarens autentiseringssession. En autentiseringstoken genereras genom att autentiserings-GUID binds till den enhet som initierar autentiseringsbegäranden.
- **Auktoriseringstoken:** Ger åtkomst till en specifik skyddad resurs som identifieras av ett unikt resurs-ID. Det består av ett auktoriseringsbidrag som utfärdats av den auktoriserande parten tillsammans med det ursprungliga resurs-ID:t. Den här informationen är bunden till den enhet som initierar begäran.
- **Kortlivad medietoken:** AccessEnabler ger åtkomst till värdprogrammet för en given resurs genom att returnera en kort medietoken. Denna token genereras baserat på den auktoriseringstoken som tidigare förvärvats för den specifika resursen. Den här variabeln är inte bunden till enheten och den associerade livslängden är betydligt kortare (standard: 5 minuter).

När autentiseringen och auktoriseringen är klar kommer Primetime-autentiseringen att utfärda autentiserings-, auktoriserings- och kortlivade medietoken. Dessa token bör cachelagras på användarens enhet och användas under hela den tid som de är kopplade till sin livstid.

 

### Riktlinjer för cachelagring {#caching}

- Autentiseringstoken
- Auktoriseringstoken
- Kortlivad medietoken


#### Autentiseringstoken

- **AccessEnabler 1.7:** Denna SDK introducerar en ny metod för tokenlagring, vilket möjliggör flera programmerings-MVPD-buffertar och därmed flera autentiseringstoken. Nu används samma lagringslayout både för scenariot Autentisering per begärande och för det normala autentiseringsflödet. Den enda skillnaden mellan de två är hur autentiseringen utförs: &quot;Autentisering per begärande&quot; innehåller en ny förbättring (passiv autentisering) som gör det möjligt för AccessEnabler att utföra autentisering i bakkanalen baserat på att det finns en autentiseringstoken i lagringen (för en annan programmerare). Användaren behöver bara autentisera en gång, och den här sessionen kommer att användas för att hämta autentiseringstoken i ytterligare appar. Detta bakkanalsflöde äger rum under [`setRequestor()`](#setReq) ringa och är för det mesta transparent för programmeraren. **Det finns dock ett viktigt krav här: Programmeraren MÅSTE anropa setRequestor() från huvudgränssnittstråden.**
- **AccessEnabler 1.6 och äldre:** Hur autentiseringstoken cachelagras på enheten beror på &quot;**Autentisering per begärande&quot;** flagga som är associerad med aktuellt MVPD:

<!-- end list -->

1. Om funktionen &quot;Autentisering per begärande&quot; är inaktiverad kommer en enda autentiseringstoken att lagras lokalt på det globala monteringsbordet. denna token delas mellan alla program som är integrerade med det aktuella MVPD-programmet.
1. Om funktionen &quot;Autentisering per begärande&quot; är aktiverad, kommer en token att uttryckligen kopplas till den programmerare som utförde autentiseringsflödet (denna token kommer inte att lagras på det globala monteringsbordet, utan i en privat fil som bara är synlig för programmerarens program). Mer specifikt kommer enkel inloggning (SSO) mellan olika program att inaktiveras. användaren måste utföra autentiseringsflödet explicit när han/hon byter till en ny app (förutsatt att programmeraren för den andra appen är integrerad med det aktuella MVPD-programmet och att det inte finns någon autentiseringstoken för programmeraren i det lokala cacheminnet).

 

#### Auktoriseringstoken

Vid en given tidpunkt cachelagras endast EN auktoriseringstoken PER RESOURCE av AccessEnabler. Det kan finnas flera autentiseringstoken cachelagrade, men de är associerade med olika resurser. När en ny auktoriseringstoken utfärdas och en gammal redan finns för *samma resurs* skriver den nya variabeln över det befintliga cachelagrade värdet.

 

#### Medietoken

Den kortlivade medietoken får INTE cachelagras alls. Medietoken bör hämtas från servern varje gång ett auktoriserings-API anropas, eftersom det är begränsat till engångsanvändning.

 

### Persistence {#persistence}

Token måste vara beständig i flera på varandra följande körningar av samma program. Detta innebär att när autentiserings- och auktoriseringstoken har hämtats och användaren stänger programmet, är samma token tillgängliga för programmet när användaren öppnar programmet igen. Dessutom är det önskvärt att dessa variabler är beständiga i flera program. När en användare har använt ett program för att logga in med en viss identitetsleverantör (har hämtat autentiserings- och auktoriseringstoken) kan samma token användas via ett annat program, och användaren uppmanas inte längre att ange autentiseringsuppgifter när han eller hon loggar in via samma identitetsleverantör. Den här typen av smidigt autentiserings-/auktoriseringsarbetsflöde gör Primetime-autentiseringslösningen till en riktig TV-Everywhere-implementering. 

 

## iOS

iOS AccessEnabler-biblioteket kan användas för att lösa problem med datadelning mellan program genom att tokendata lagras i en&quot;urklippsliknande&quot; datastruktur som kallas för *paste board*. Den här delade resursen på systemnivå innehåller nyckelkomponenter som gör att det går att implementera de önskade permanenta token som ska användas:

- **Stöd för strukturerad lagring** - Klistra in är inte bara en enkel, linjär buffertliknande minnesstruktur. Den innehåller en ordlisteliknande lagringsmekanism som gör det möjligt att indexera data baserat på användarspecificerade nyckelvärden.
- **Stöd för databeständighet med hjälp av det underliggande filsystemet** - Innehållet i paste board-strukturen kan markeras som beständig. I så fall sparas data på enhetens interna minne.

 

När en viss token har placerats i token-cachen kontrolleras dess giltighet vid olika tillfällen av AccessEnabler-biblioteket.  En giltig token definieras som:

- Token har inte gått ut.
- Utfärdaren av token ingår i listan över tillåtna identitetsleverantörer.

 

## tvOS

Eftersom monteringsbordet inte är tillgängligt på tvOS använder biblioteket tvOS AccessEnabler NsUserDefaults som lagringsalternativ. Detta löser problemet med beständiga autentiserings- och behörighetstoken, men den lagrade informationen kan inte delas mellan olika program.

 

**Ändringar av monteringsbordet i iOS 10 -** När du uppgraderar från en tidigare version av iOS raderas monteringsbordet. Det innebär att alla program måste autentiseras på nytt.

 

**Ändringar av monteringsbordet i iOS 7 -** På grund av förändringar i hur monteringsbord fungerar i iOS 7 kommer det att finnas begränsad korsinloggning mellan program som körs i iOS 7. Program som har samma `<Bundle Seed ID>`(kallas även `<Team ID>`) delar tokens, vilket innebär att program A1 och A2 från samma programmerare X delar tokens, medan program A1 (Programmer X) och program A3 (Programmer Y) inte delar tokens. 

- Källpaket-ID/Team-ID är samma mellan två program om de genereras av samma provisioneringsprofil. Här hittar du mer information:
   [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html ](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- Den här begränsningen för enkel inloggning (Cross SSO) finns i iOS 7 oavsett vilken SDK för autentisering av Primetime som används. 

Läs den här tekniska kommentaren för mer information om hur du konfigurerar enkel inloggning på iOS 7 och senare (Tech note apply for Access Enabler v1.8 och senare): <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>

 

### Tokenlagring (AccessEnabler 1.7)

Från och med AccessEnabler 1.7 kan tokenlagringen ha stöd för flera programmerings-MVPD-kombinationer, beroende på en kapslad mappningsstruktur på flera nivåer som kan innehålla flera autentiseringstoken. Det nya lagringsutrymmet påverkar inte det offentliga API:t för AccessEnabler på något sätt och kräver inga ändringar från programmeraren. Här är ett exempel som illustrerar den här nya funktionen:

1. Öppna App1 (utvecklad av Programmer1).
1. Autentisera med MVPD1 (som är integrerad med Programmer1).
1. Skjut upp/stäng det aktuella programmet och öppna App2 (utvecklad av Programmer2).
1. Låt oss anta att Programmer2 inte är integrerat med MVPD2. Därför kommer användaren INTE att autentiseras i App2.
1. Autentisera med MVPD2 (som är integrerat med Programmer2) i App2.
1. Växla tillbaka till App1. Användaren autentiseras fortfarande med Programmer1.

I äldre versioner av AccessEnabler återges användaren som icke-autentiserad i steg 6, eftersom tokenlagringen tidigare bara hade stöd för en autentiseringstoken.

 

Om du loggar ut från en programmerare/MVPD-session rensas hela det underliggande lagringsutrymmet, inklusive alla andra autentiseringstoken för programmerare/MVPD på enheten. Å andra sidan avbryts autentiseringsflödet (anropar [`setSelectedProvider(null)`](#setSelProv)) rensar INTE det underliggande lagringsutrymmet, men det påverkar bara det aktuella autentiseringsförsöket för Programmer/MVPD (genom att radera det MVPD för den aktuella programmeraren).

 

### Tokenimporterare (AccessEnabler 1.7)

En annan lagringsrelaterad funktion som ingår i AccessEnabler 1.7 gör det möjligt att importera autentiseringstoken från äldre lagringsområden. Den här&quot;tokenimporteraren&quot; hjälper till att uppnå kompatibilitet mellan efterföljande AccessEnabler-versioner och upprätthålla SSO-läget även när lagringsversionen uppgraderas. Importören utförs under [`setRequestor()`](#setReq) flödar och körs i följande två scenarier (förutsatt att det inte finns någon giltig autentiseringstoken för den aktuella programmeraren i det aktuella lagringsutrymmet):

- Den första installationen av en 1.7-app som har utvecklats av en specifik programmerare
- Uppgraderingsväg till en framtida AccessEnabler som använder en ny lagringsplats

Importåtgärden är genomskinlig för programmeraren och kräver ingen kodändring i klientprogrammet.

 

### Token Sanitizer (AccessEnabler 1.7.5)

Från och med AccessEnabler 1.7.5 kan den här tjänsten köras på [`setRequestor()`](#setReq)`. `Den utvecklades som ett resultat av iOS 7-bytet från WiFi MAC-adressen till IDFA för spårning. Sanitizer ser till att den aktuella lagringen bara innehåller giltiga autentiseringstoken (giltiga för enhets-ID, som tidigare beräknats med MAC-adressen, före iOS7). Token Sanitizer tar bort alla ogiltiga tokens. 

 

Token Sanitizer-tjänsten är mest användbar när ett AccessEnabler 1.7.5-program används i iOS 6 och sedan uppdaterar användaren till iOS 7. När detta inträffar blir alla autentiseringstoken som hämtades på iOS 6 ogiltiga (på grund av att algoritmen för enhets-ID ändras från att använda MAC-adressen till IDFA). Sanitizer rensar alla ogiltiga tokens och användaren blir då oautentiserad. 

 

Om inte Token Sanitizer tar bort ogiltiga tokens kan AccessEnabler inte erhålla auktoriseringar på grund av ogiltiga autentiseringstoken. Detta skulle visa sig vara svårt för slutanvändaren att felsöka, eftersom verifieringsfelmeddelanden kan vara kryptiska och inte alltför användbara för att avgöra vad som orsakade problemet. 

 

### Format {#format}

- [AuthN-token](#authn_token)
- [AuthZ-token](#authz_token)
- [Kort medietoken](#short_token)
- [Enhetsbindning](#device_binding)


Observera att formatet för AuthN- och AuthZ-tokens inkluderas här endast för bakgrundsinformation. Strukturen för dessa tokens kan när som helst ändras med Primetime-autentisering. Programmerare behöver inte känna till den exakta strukturen för AuthN- och AuthZ-tokens för att implementera sina appar, eftersom AuthN- och AuthZ-tokens inte visas på den lokala enheten. Kort medietoken *är* exponeras för programmerarens program.

 

#### Autentiseringstoken {#authn_token}

I listan nedan visas formatet för autentiseringstoken:

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthenticationToken>
      <simpleTokenAuthenticationGuid>71C69B91-F327-F185-F29E-2CE20DC560F5</simpleTokenAuthenticationGuid>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenDomainName>adobe.com</simpleTokenDomainName>
      <simpleTokenExpires>2011/03/19 02:29:34 GMT +0200</simpleTokenExpires>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>   
  </simpleAuthenticationToken>
```
 

#### Auktoriseringstoken {#authz_token}

I listan nedan visas auktoriseringstokens format:

```
  <signatureInfo>base64(...)<signatureInfo>
  <simpleAuthorizationToken>
      <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
      <simpleTokenResourceID>TEST_RESOURCE</simpleTokenResourceID>
      <simpleTokenTTL>2011/03/17 14:40:08 GMT +0200</simpleTokenTTL>
      <simpleTokenMsoID>Adobe</simpleTokenMsoID>
      <simpleTokenDeviceID>
          <simpleTokenFingerprint>
              HASH(true device identification info)
          </simpleTokenFingerprint>
      </simpleTokenDeviceID>
  </simpleAuthorizationToken>
```
 

#### Kort medietoken {#short_token}

I listan nedan visas formatet för den korta medietoken. Den här variabeln visas för programmerarens program. Det skickas till Programmerarens program när en tillståndsprocess är slutförd:

```
  <signatureInfo>signature<signatureInfo>
  <shortAuthorizationToken>
    <sessionGUID>session_guid</sessionGUID>
    <requestorID>requestor_id</requestorID>
    <resourceID>resource_id</resourceID>
    <ttl>ttl_in_ms</ttl>
    <issueTime>issue_time</issueTime>
    <mvpdId>mvpd_id</mvpdId>
    <proxyMvpdId>proxy_mvpd_id</proxyMvpdId>
  </shortAuthorizationToken>
```
 

### Enhetsbindning {#device_binding}

Observera taggen med titeln i XML-listan ovan `simpleTokenFingerprint`. Syftet med den här taggen är att lagra information om anpassad enhets-ID. AccessEnabler-biblioteket kan hämta sådan individualiseringsinformation och göra den tillgänglig för Primetimes autentiseringstjänster under berättigandeanropen. Tjänsten kommer att använda den här informationen och bädda in den i de faktiska tokenerna, vilket effektivt binder tokenerna till en viss enhet. Slutmålet för detta är att göra tokens icke-överförbara över olika enheter.

 

Eftersom detta är en uppenbart säkerhetsrelaterad funktion är denna information i sig&quot;känslig&quot; ur säkerhetssynpunkt. Därför måste denna information skyddas mot både manipulering och tjuvlyssning. Eavesdropping-problemet löses genom att autentiserings-/auktoriseringsbegäranden skickas via HTTPS-protokollet. Manipuleringsskyddet hanteras genom att enhetsidentifieringsinformationen signeras digitalt. AccessEnabler-biblioteket beräknar ett enhets-ID från information som anges av enheten och skickar sedan enhets-ID:t &quot;i klartext&quot; till Primetimes autentiseringsservrar som en begärandeparameter. Primetimes autentiseringsservrar signerar digitalt enhets-ID med Adobe privat nyckel och lägger till det i den autentiseringstoken som returneras till AccessEnabler. Detta innebär att enhets-ID är bundet till autentiseringstoken. Under auktoriseringsflödet skickar AccessEnabler igen enhets-ID:t i rensningen tillsammans med autentiseringstoken. Om valideringsprocessen misslyckas kommer autentiserings-/auktoriseringsarbetsflödena automatiskt att misslyckas. Primetimes autentiseringsservrar använder den privata nyckeln för enhets-ID och jämför den med värdet i autentiseringstoken. Om de inte matchar misslyckas tillståndsflödet.

 

**Note on Device Binding in AccessEnabler 1.7.5:** Från och med AccessEnabler 1.7.5 ändras hur enhets-ID beräknas för att ange personaliseringsinformation för en iOS-enhet. Ändringen återspeglar en förändring i iOS 7: Från iOS 7 tillhandahåller Apple inte längre WiFi MAC-adressen som ett spårningsalternativ, till förmån för IDFA (Identifier for Advertisers). Eftersom personaliseringsinformation för en app som körs på iOS 7 baseras på IDFA och den informationen är inbäddad i tillståndsflödestoken innebär detta att det finns ett antal olika möjliga effekter på användarupplevelsen som följer av den här ändringen. Olika effekter baseras på vilken version av iOS som användaren uppgraderar från och vilken version av AccessEnabler som programmeraren uppgraderar från. Mer information om den här ändringen finns i versionsinformationen som ingår i AccessEnabler SDK 1.7.5.

<!--
## Related Information {#related}


- [iOS/tvOS Integration Cookbook](#)
- [iOS/tvOS API Reference](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Primetime
  authentication native SDK (Tech Note)](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [SSO on iOS when using the Primetime authentication Access
  Enabler](#)
-->
