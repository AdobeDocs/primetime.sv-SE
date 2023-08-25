---
title: Amazon FireOS Technical Overview
description: Amazon FireOS Technical Overview
exl-id: 939683ee-0dd9-42ab-9fde-8686d2dc0cd0
source-git-commit: 4691e769e1fee51507550c8e1fbecdcdff7e44eb
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 0%

---

# Amazon FireOS Technical Overview {#amazon-fireos-technical-overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

</br>

## Introduktion {#intro}

Amazon FireOS AccessEnabler representeras av två komponenter: ett AccessEnabler-stub-bibliotek som används av programmet och ett Java Android-bibliotek på systemnivå som gör det möjligt för mobilappar att använda Adobe Primetime-autentisering för TV Everywhere-berättigandetjänster. En Android-implementering för Amazon FireOS består av AccessEnabler-gränssnittet som definierar berättigande-API:t och ett EntitlementDelegate-protokoll som beskriver återanropen som biblioteket utlöser. Med AccessEnabler Android-biblioteket på systemnivå kan du få åtkomst till Amazon tjänster och aktivera enkel inloggning på plattformsnivå.

## Understanding Native Client Workflows {#native_client_workflows}

Inbyggda klientarbetsflöden är vanligtvis desamma som, eller mycket liknande, de som gäller för webbläsarbaserade Primetime-autentiseringsklienter. Det finns dock några undantag, som beskrivs nedan.


### Arbetsflöde efter initiering {#post-init}

Alla tillståndsarbetsflöden som stöds av AccessEnabler förutsätter att du tidigare har anropat [`setRequestor()`](#setRequestor) för att fastställa din identitet. Du gör det här anropet för att bara ange ditt begärande-ID en gång, vanligtvis under programmets initierings-/installationsfas.

Med inbyggda klienter (t.ex. AmazonFireOS) efter ditt första anrop till [`setRequestor()`](#setRequestor)kan du välja hur du vill fortsätta:

- Du kan börja ringa berättigandesamtal direkt och låta dem stå i kö om det behövs.
- Du kan också få en bekräftelse på om [`setRequestor()`](#setRequestor) genom att implementera callback-funktionen setRequestorComplete().
- Eller gör båda.

Det är upp till er att vänta på att ni ska meddela om det lyckades [`setRequestor()`](#setRequestor) eller för att förlita dig på AccessEnablers anropskömekanism. Eftersom alla efterföljande autentiserings- och autentiseringsbegäranden behöver begärande-ID och associerad konfigurationsinformation kan [`setRequestor()`](#setRequestor) metoden blockerar effektivt alla API-anrop för autentisering och auktorisering tills initieringen är slutförd.

### Allmänt inledande autentiseringsarbetsflöde {#generic}

Syftet med det här arbetsflödet är att logga in en användare med sitt MVPD-program.  När inloggningen är klar utfärdar backend-servern en autentiseringstoken till användaren. Autentisering sker vanligtvis som en del av auktoriseringsprocessen, men följande beskriver hur autentisering kan fungera fristående och inkluderar inga auktoriseringssteg.

Observera att även om följande inbyggda klientarbetsflöde skiljer sig från det vanliga webbläsarbaserade autentiseringsarbetsflödet är steg 1-5 samma för både inbyggda klienter och webbläsarbaserade klienter:

1. Sidan eller spelaren initierar autentiseringsarbetsflödet med ett anrop till [getAuthentication()](#getAuthN)som söker efter en giltig cachelagrad autentiseringstoken. Den här metoden har ett valfritt värde `redirectURL` parameter; om du inte anger något värde för `redirectURL`efter en lyckad autentisering returneras användaren till den URL som autentiseringen initierades från.
1. AccessEnabler avgör aktuell autentiseringsstatus. Om användaren är autentiserad anropar AccessEnabler `setAuthenticationStatus()` callback-funktion, skicka en autentiseringsstatus som indikerar att åtgärden lyckades (steg 7 nedan).
1. Om användaren inte är autentiserad fortsätter AccessEnabler autentiseringsflödet genom att fastställa om användarens senaste autentiseringsförsök lyckades med ett visst MVPD. Om ett MVPD ID cachelagras OCH `canAuthenticate` flaggan är true ELLER så har ett MVPD valts med [`setSelectedProvider()`](#setSelectedProvider)visas inte dialogrutan för MVPD-val. Autentiseringsflödet fortsätter med det cachelagrade värdet för MVPD (det vill säga samma MVPD som användes vid den senaste autentiseringen). Ett nätverksanrop görs till serverdelen och användaren omdirigeras till inloggningssidan för MVPD (steg 6 nedan).
1. Om inget MVPD ID cachelagras OCH inget MVPD valdes med [`setSelectedProvider()`](#setSelectedProvider) ELLER `canAuthenticate` flaggan är inställd på false, [`displayProviderDialog()`](#displayProviderDialog) återanrop anropas. I det här återanropet dirigeras sidan eller spelaren till det användargränssnitt som visar en lista över PDF-filer som användaren kan välja mellan. En array med MVPD-objekt tillhandahålls, som innehåller den information som krävs för att du ska kunna skapa MVPD-väljaren. Varje MVPD-objekt beskriver en MVPD-enhet och innehåller information om exempelvis MVPD-filens ID (t.ex. XFINITY, AT\&amp;T) och den URL där MVPD-logotypen finns.
1. När ett visst MVPD-dokument har valts måste sidan eller spelaren informera AccessEnabler om användarens val. För klienter som inte är Flashar informerar du AccessEnabler om användarvalet via ett anrop till [`setSelectedProvider()`](#setSelectedProvider) -metod. Flash-klienter skickar i stället en delad `MVPDEvent` av typen &quot;`mvpdSelection`&quot;, skickar den markerade providern.
1. För Amazon [`navigateToUrl()`](#navigagteToUrl) återanrop ignoreras. Biblioteket Access Enabler ger åtkomst till en gemensam WebView-kontroll som autentiserar användare.
1. Via `WebView`, kommer användaren till MVPD:s inloggningssida och anger sina inloggningsuppgifter. Observera att flera omdirigeringsåtgärder utförs under den här överföringen.
1. När WebView-kontrollen har slutfört autentiseringen stängs den och informerar AccessEnabler om att användaren har loggat in, så hämtar AccessEnabler den faktiska autentiseringstoken från backend-servern. AccessEnabler anropar [`setAuthenticationStatus()`](#setAuthNStatus) återanrop med statuskoden 1, vilket anger att det lyckades. Om det uppstår ett fel under körningen av dessa steg [`setAuthenticationStatus()`](#setAuthNStatus) återanrop aktiveras med statuskoden 0, tillsammans med motsvarande felkod, vilket anger att användaren inte är autentiserad.

### Utloggningsarbetsflöde {#logout}

För inbyggda klienter hanteras inloggningar på liknande sätt som autentiseringsprocessen som beskrivs ovan. I det här mönstret skapar AccessEnabler en `WebView` och läser in kontrollen med URL:en för utloggningsslutpunkten på backend-servern. När utloggningsprocessen är slutförd rensas token.

Observera att utloggningsflödet skiljer sig från autentiseringsflödet eftersom användaren inte behöver interagera med `WebView` på något sätt. När utloggningen är klar anropar AccessEnabler `setAuthenticationStatus()` återanrop med statuskoden 0, vilket anger att användaren inte är autentiserad.

## Tokens {#tokens}

### Definitioner och användning {#definitions}

Primetimes behörighetslösning för autentisering gäller generering av specifika datadelar (tokens) som genereras av Primetime-autentisering när autentiserings- och auktoriseringsarbetsflödena har slutförts. Dessa token lagras lokalt på klientens Amazon FireOS-enhet.

Tokens har begränsad livslängd. När den upphör att gälla måste tokens utfärdas på nytt genom att autentiserings- och/eller auktoriseringsarbetsflödena återupptas.

Det finns tre typer av tokens som utfärdas under tillståndsarbetsflödena:

- **Autentiseringstoken** - Slutresultatet av användarautentiseringsarbetsflödet blir ett autentiserings-GUID som AccessEnabler kan använda för att göra auktoriseringsfrågor för användarens räkning. Detta autentiserings-GUID har ett associerat TTL-värde (time-to-live) som kan skilja sig från användarens autentiseringssession. Primetime-autentisering genererar en autentiseringstoken genom att binda autentiserings-GUID till den enhet som initierar autentiseringsbegäranden.
- **Auktoriseringstoken** - Ger åtkomst till en specifik skyddad resurs som identifieras av en unik `resourceID`. Det består av ett tillståndsbidrag som utfärdats av den tillståndsgivande parten tillsammans med originalet `resourceID`. Den här informationen är bunden till den enhet som initierar begäran.
- **Kortlivad medietoken** - AccessEnabler ger åtkomst till värdprogrammet för en given resurs genom att returnera en kortlivad medietoken. Denna token genereras baserat på den auktoriseringstoken som tidigare förvärvats för just den aktuella resursen. Den här token är inte bunden till enheten och den associerade livstiden är betydligt kortare (standard: 5 minuter).

När autentiseringen och auktoriseringen är klar kommer Primetime-autentiseringen att utfärda autentiserings-, auktoriserings- och kortlivade medietoken. Dessa token bör cachelagras på användarens enhet och användas under hela den tid som de är kopplade till sin livstid.

### Riktlinjer för cachelagring {#caching}


#### Autentiseringstoken

- **AccessEnabler 1.10.1 för FireOS** är baserat på AccessEnabler för Android 1.9.1 - SDK introducerar en ny metod för tokenlagring, vilket möjliggör flera programmerings-MVPD-bucket och därmed flera autentiseringstoken.

#### Auktoriseringstoken

Vid ett givet tillfälle cachelagras bara EN auktoriseringstoken per resurs av AccessEnabler. Det kan finnas flera autentiseringstoken cachelagrade, men de är associerade med olika resurser. När en ny auktoriseringstoken utfärdas och en gammal redan finns för samma resurs, skriver den nya token över det befintliga cachelagrade värdet.

#### Medietoken

Den kortlivade medietoken får INTE cachelagras alls. Medietoken bör hämtas från servern varje gång ett auktoriserings-API anropas, eftersom det är begränsat till engångsanvändning.

### Persistence {#persistence}

Token måste vara beständig i flera på varandra följande körningar av samma program. Detta innebär att när autentiserings- och auktoriseringstoken har hämtats och användaren stänger programmet, är samma token tillgängliga för programmet när användaren öppnar programmet igen. Dessutom är det önskvärt att dessa variabler är beständiga i flera program. När en användare har använt ett program för att logga in med en viss identitetsleverantör (har hämtat autentiserings- och auktoriseringstoken) kan samma token användas via ett annat program, och användaren uppmanas inte längre att ange autentiseringsuppgifter när han eller hon loggar in via samma identitetsleverantör.

Den här typen av smidigt autentiserings-/auktoriseringsarbetsflöde gör Primetime-autentiseringslösningen till en riktig TV-Everywhere-implementering. Ur en rent teknisk synvinkel kan Android AccessEnabler-biblioteket kringgå problemen med datadelning mellan program genom att lagra tokendata i en databasfil som finns på en extern lagringsplats. Dessa delade resurser på systemnivå innehåller de viktigaste komponenterna som gör det möjligt att implementera de önskade permanenta token-användningsexemplen:

- Stöd för strukturerad lagring - Primetimes tokenlagring för autentisering är inte bara en enkel linjär buffertliknande minnesstruktur. Den innehåller en ordlisteliknande lagringsmekanism som gör det möjligt att indexera data baserat på användarspecificerade nyckelvärden.
- Stöd för databeständighet med det underliggande filsystemet - innehållet i databasfilen bevaras som standard och data sparas på enhetens externa minne.

När en viss token har placerats i token-cachen kontrolleras dess giltighet vid olika tillfällen av AccessEnabler-biblioteket.  En giltig token definieras som:

- Token har inte gått ut
- Utfärdaren av token ingår i listan över tillåtna identitetsleverantörer

Token Storage kan hantera flera programmerings-MVPD-kombinationer, beroende på en kapslad mappstruktur på flera nivåer som kan innehålla flera autentiseringstoken. Det nya lagringsutrymmet påverkar inte det offentliga API:t för AccessEnabler på något sätt och kräver inga ändringar från programmerarens sida. Här följer ett exempel som visar den här nyare funktionen:

1. Öppna App1 (utvecklad av Programmer1).
1. Autentisera med MVPD1 (som är integrerad med Programmer1).
1. Skjut upp/stäng det aktuella programmet och öppna App2 (utvecklad av Programmer2).
1. Låt oss anta att Programmer2 inte är integrerat med MVPD2. Därför kommer användaren INTE att autentiseras i App2.
1. Autentisera med MVPD2 (som är integrerat med Programmer2) i App2.
1. Växla tillbaka till App1. Användaren autentiseras fortfarande med Programmer1.

### Format {#format}

#### Autentiseringstoken {#authn_token}

I listan nedan visas formatet för autentiseringstoken:

```JSON
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

```JSON
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


#### Kort medietoken {#short_media_token}

I listan nedan visas formatet för den korta medietoken.  Denna token visas för programmerarens program.  Det skickas till Programmerarens program när en tillståndsprocess är slutförd:

```JSON
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


#### Enhetsbindning {#device_binding}

Observera taggen med titeln i XML-listan ovan `simpleTokenFingerprint`. Syftet med den här taggen är att lagra information om anpassad enhets-ID. AccessEnabler-biblioteket kan hämta sådan individualiseringsinformation och göra den tillgänglig för Primetimes autentiseringstjänster under berättigandeanropen. Tjänsten kommer att använda den här informationen och bädda in den i de faktiska tokenerna, vilket effektivt binder tokenerna till en viss enhet. Slutmålet för detta är att göra tokens icke-överförbara över olika enheter.

Observera taggen simpleTokenFingerprint i XML-listan ovan. Syftet med den här taggen är att lagra information om anpassad enhets-ID. AccessEnabler-biblioteket kan hämta sådan individualiseringsinformation och göra den tillgänglig för Primetimes autentiseringstjänster under berättigandeanropen. Tjänsten kommer att använda den här informationen och bädda in den i de faktiska tokenerna, vilket effektivt binder tokenerna till en viss enhet. Slutmålet för detta är att göra tokens icke-överförbara över olika enheter.

Eftersom detta är en uppenbart säkerhetsrelaterad funktion är denna information i sig&quot;känslig&quot; ur säkerhetssynpunkt. Därför måste denna information skyddas mot både manipulering och tjuvlyssning. Eavesdropping-problemet löses genom att autentiserings-/auktoriseringsbegäranden skickas via HTTPS-protokollet. Manipuleringsskyddet hanteras genom att enhetsidentifieringsinformationen signeras digitalt. AccessEnabler-biblioteket beräknar ett enhets-ID från information som anges av enheten och skickar sedan enhets-ID:t &quot;i klartext&quot; till Primetimes autentiseringsservrar som en begärandeparameter.  Primetimes autentiseringsservrar signerar digitalt enhets-ID med Adobe privat nyckel och lägger till det i den autentiseringstoken som returneras till AccessEnabler. Detta innebär att enhets-ID är bundet till autentiseringstoken.  Under auktoriseringsflödet skickar AccessEnabler igen enhets-ID:t i rensningen tillsammans med autentiseringstoken.  Om valideringsprocessen misslyckas kommer det automatiskt att leda till att arbetsflödena för autentisering/auktorisering misslyckas.  Primetimes autentiseringsservrar använder den privata nyckeln för enhets-ID och jämför den med värdet i autentiseringstoken.  Om de inte matchar misslyckas tillståndsflödet.
