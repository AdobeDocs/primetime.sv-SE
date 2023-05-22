---
title: Android SDK med registrering av dynamisk klient
description: Android SDK med registrering av dynamisk klient
exl-id: 8d0c1507-8e80-40a4-8698-fb795240f618
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1294'
ht-degree: 0%

---

# Android SDK med registrering av dynamisk klient {#android-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion {#Intro}

Android AccessEnabler SDK för Android har ändrats för att aktivera autentisering utan att använda sessionscookies. I takt med att fler och fler webbläsare begränsar åtkomsten till cookies måste en annan metod användas för att tillåta autentisering.

För Android begränsar användningen av anpassade flikar i Chrome åtkomsten till cookies från andra program.

>**Android SDK 3.0.0** introducerar:

- dynamisk klientregistrering ersätter den aktuella appregistreringsmekanismen baserat på autentisering av signerad begärande-ID och sessionscookie
- Krom anpassade flikar för autentiseringsflöden

>[!NOTE]
>
>För äldre Android-versioner utan stöd för anpassade Chrome-flikar används WebView-autentiseringen på samma sätt som i äldre AccessEnabler SDK-versioner.


## Dynamisk klientregistrering {#DCR}

Android SDK v3.0+ använder den dynamiska klientregistreringsproceduren som definieras i [Dynamisk klientregistrering](/help/authentication/dynamic-client-registration.md).


## Demo {#Demo}

Titta [det här webbinariet](https://my.adobeconnect.com/pzkp8ujrigg1/) som ger ett större sammanhang för funktionen och innehåller en demonstration av hur programsatser ska hanteras med TVE Dashboard och hur de genererade programsatserna ska testas med ett demoprogram som tillhandahålls av Adobe som en del av Android SDK.

## API-ändringar {#API}


### Factory.getInstance

**Beskrivning:** Instansierar Access Enabler-objektet. Det ska finnas en enda instans av Access Enabler per programinstans.

| API-anrop: konstruktor |
| --- |
| public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        returnerar AccessEnablerException |


**Tillgänglighet:** v3.0+

**Parametrar:**

- *appContext*: Android-programkontext
- softwareStatement: värde från TVE Dashboard eller *null* om &quot;software\_statement&quot; är inställt i strings.xml
- redirectUrl : unik URL, en av domänerna i omvänd ordning som uttryckligen lades till i TVE Dashboard eller *null* om &quot;redirect\_uri&quot; har angetts i strings.xml

Obs! ogiltig softwareStatement eller redirectUrl kommer att göra att programmet inte initierar AccessEnabler eller registrerar program för autentisering och auktorisering av Adobe Pass
</br>
Obs! redirectUrl-parametern eller redirect\_uri i strings.xml ska vara värdet på domänen som läggs till i TVE Dashboard för programmet i omvänd ordning (till exempel: för domänen adobe.com som läggs till i TVE Dashboard ska redirectUrl vara com.adobe.
 

### setRequestor

**Beskrivning:** Fastställer kanalens identitet. Varje kanal tilldelas ett unikt ID när den registreras med Adobe för Adobe Primetime autentiseringssystem. När det gäller enkel inloggning och fjärrtoken kan autentiseringstillståndet ändras när programmet är i bakgrunden. Det går att anropa setRequestor igen när programmet försätts i förgrunden för att synkronisera med systemtillståndet (hämta en fjärrtoken om enkel inloggning är aktiverad eller ta bort den lokala token om en utloggning inträffar under tiden).

Serversvaret innehåller en lista över MVPD:er tillsammans med viss konfigurationsinformation som är kopplad till kanalens identitet. Serversvaret används internt av åtkomstaktiveringskoden. Endast åtgärdens status (d.v.s. SUCCESS/FAIL) visas för programmet via callback-funktionen setRequestorComplete().

Om *urls* parametern används inte, det resulterande nätverksanropet har standardtjänstleverantörens URL som mål: Adobe-versionen/produktionsmiljön.

Om ett värde anges för *urls* parametern, aktiverar det resulterande nätverksanropet alla URL:er som anges i *urls* parameter. Alla konfigurationsbegäranden aktiveras samtidigt i olika trådar. Den första svararen har företräde när listan över MVPD kompileras. För varje MVPD i listan kommer åtkomstaktiveringen att komma ihåg URL:en för den associerade tjänstleverantören. Alla efterföljande tillståndsbegäranden dirigeras till den URL som är associerad med tjänstleverantören som parats med mål-MVPD under konfigurationsfasen.

| API-anrop: begärandekonfiguration |
| --- |
| ```public void setRequestor(String requestorId)``` |

**Tillgänglighet:** v3.0+

| API-anrop: begärandekonfiguration |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**Tillgänglighet:** v3.0+

**Parametrar:**

- *requestID*: Det unika ID som är associerat med kanalen. Skicka det unika ID som tilldelats av Adobe till din webbplats när du först registrerade dig för Adobe Primetime autentiseringstjänst.
- *urls*: Valfri parameter Adobes tjänsteleverantör används som standard [http://sp.auth.adobe.com/](http://sp.auth.adobe.com/). Med den här arrayen kan du ange slutpunkter för autentisering och auktoriseringstjänster som tillhandahålls av Adobe (olika instanser kan användas i felsökningssyfte). Du kan använda detta för att ange flera instanser av Adobe Primetime-autentiseringstjänster. När detta görs består MVPD-listan av slutpunkterna från alla tjänsteleverantörer. Varje separat skyddsbehövande dokument är knutet till den snabbaste tjänsteleverantören. det vill säga den leverantör som svarade först och som stöder det MVPD.

Föråldrat:

- *signedRequestorID*: En kopia av begärande-ID som signeras digitalt med din privata nyckel. <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**Återanrop utlösta:** `setRequestorComplete()`

### utloggning

**Beskrivning:** Använd den här metoden för att initiera utloggningsflödet. Utloggningen är resultatet av en serie HTTP-omdirigeringsåtgärder på grund av att användaren måste loggas ut både från Adobe Primetime autentiseringsservrar och från MVPD-servrarna. Det innebär att det här flödet öppnar ett ChromeCustomTab-fönster för att köra utloggningen.

| API-anrop: initiera utloggningsflödet |
| --- |
| public void log() |

**Tillgänglighet:** v3.0+

**Parametrar:** Ingen

**Återanrop utlösta:** `setAuthenticationStatus()`
</br></br>

## Programmeringsimplementeringsflöde {#Progr}

### **1. Registrera program** 

a. Hämta software\_statement och redirect\_uri från Adobe Pass ( TVE Dashboard )

b. Det finns två alternativ för att skicka dessa värden till Adobe Pass SDK:

Lägg till i strings.xml: 

```XML
<string name="software_statement">[softwarestatement value]</string>
<string name="redirect_uri">application_url.com</string>
```

Anropa AccessEnabler.getInstance(appContext,softwareStatement, redirectUrl)


### 2. Konfigurera program

a. setRequestor(request\_id) 

SDK kommer att utföra följande åtgärder: 

- registerprogram: använda **software\_statement** får SDK en **client\_id, client\_secrets, client\_id\_issued\_at, redirect\_uris, grant\_types**. Den här informationen lagras i programmets interna lagring.

- få en **access\_token** med client\_id, client\_secrets och grant\_type=&quot;client\_credentials&quot;. Denna åtkomst\_token kommer att användas för varje anrop från SDK till Adobe Pass-servrar 

**Tokenfelsvar:**

| Felsvar |  |  |
| --- | --- | --- |
| HTTP 400 (Ogiltig begäran) | {&quot;error&quot;: &quot;invalid\_request&quot;} | Begäran saknar en obligatorisk parameter, innehåller ett parametervärde som inte stöds (annat än anslagstyp), upprepar en parameter, innehåller flera autentiseringsuppgifter, använder mer än en mekanism för autentisering av klienten eller har på annat sätt fel format. |
| HTTP 400 (Ogiltig begäran) | {&quot;error&quot;: &quot;invalid\_client&quot;} | Klientautentiseringen misslyckades eftersom klienten var okänd. SDK MÅSTE registreras på auktoriseringsservern igen. |
| HTTP 400 (Ogiltig begäran) | {&quot;error&quot;: &quot;unauthorized\_client&quot;} | Den autentiserade klienten har inte behörighet att använda den här behörighetstypen. |

- om ett MVPD-dokument kräver passiv autentisering öppnas en anpassad flik i Chrome så att den körs passivt med detta MVPD-dokument och stängs när det är klart

b. checkAuthentication()

- true : gå till Authorization
- false : gå till Select MVPD

c. getAuthentication : SDK inkluderar **access_token** i anropsparametrar 

- mvpd kom ihåg : gå till setSelectedProvider(mvpd_id)
- mvpd inte vald: displayProviderDialog
- mvpd valt: gå till setSelectedProvider(mvpd_id)

d. setSelectedProvider

- mvpd\_id-autentiserings-url har lästs in i ChromeCustomTabs
- inloggningen lyckades: delegate.setAuthenticationStatus ( SUCCESS )
- Inloggningen avbröts: återställ MVPD-val
- URL-schemat har etablerats som &quot;adobepass://redirect_uri&quot; för hämtning när autentiseringen är klar

e. get/checkAuthorization: SDK inkluderar **access_token** i rubriken som auktorisering: Bearer **access_token**

- om auktoriseringen lyckas, kommer ett anrop att göras för att erhålla medietoken

f. loggout: 

- SDK kommer att ta bort giltig token för den aktuella begäraren (autentiseringar som erhållits av andra program och inte via enkel inloggning kommer att förbli giltiga)
- SDK öppnar anpassade Chrome-flikar för att nå mvpd_id-utloggningsslutpunkten. När du är klar stängs de anpassade Chrome-flikarna
- URL-schemat är &quot;adobepass://logout&quot; för att fånga in tidpunkten då utloggningen är klar
- utlöser en sendTrackingData(new Event(EVENT_LOGOUT,USER_NOT_AUTHENTICATED_ERROR) och ett återanrop: setAuthenticationStatus(0,&quot;Logout&quot;)

**Obs!** eftersom varje samtal kräver **access_token,** Möjliga felkoder nedan hanteras i SDK. 


| Felsvar |  |  |
| --- | ---|--- |
| invalid_request | 400 | Begäran har fel format. SDK:n bör sluta utföra anrop till servern. |
| invalid_client | 403 | Klient-ID:t har inte längre behörighet att utföra begäranden. SDK MÅSTE utföra klientregistreringen igen. |
| access_deny | 401 | Åtkomst\_token är inte giltig. SDK MÅSTE begära en ny access_token. |
