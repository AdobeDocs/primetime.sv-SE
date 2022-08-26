---
title: REST API Cookbook (klient-till-server)
description: Återställ API-cookbook-klienten till servern.
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 1%

---


# REST API Cookbook (klient-till-server) {#rest-api-cookbook-client-to-server}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.


## Översikt {#overview}

Det här dokumentet innehåller stegvisa instruktioner för programmerarens tekniker att integrera en&quot;smart enhet&quot; (spelkonsol, smart TV-app, digitalbox osv.) med Adobe Primetime-autentisering med REST API-tjänster. Denna klient-till-server-metod, som använder REST-API:er i stället för en klient-SDK, ger bredare stöd för olika plattformar där det inte skulle vara möjligt att utveckla ett stort antal unika SDK:er. En utförlig teknisk översikt över hur den klientlösa lösningen fungerar finns i [Kundfri teknisk översikt](/help/authentication/rest-api-overview.md).


Strategin kräver två komponenter (direktuppspelningsapp och AuthN-app) för att slutföra de nödvändiga flödena: start-, registrerings-, auktoriserings- och vymedieflöden i direktuppspelningsappen och autentiseringsflödet i din AuthN-app.

## Komponenter {#components}

I en fungerande klient-till-server-lösning ingår följande komponenter:

 

| Typ | Komponent | Beskrivning |
| --- | --- | --- |
| Strömmande enhet | Strömmande app | Programmeringsprogrammet som finns på användarens direktuppspelningsenhet och spelar upp autentiserad video. |
|  | \[Valfritt\] AuthN-modul | Om direktuppspelningsenheten har en användaragent (t.ex. en webbläsare) ansvarar AuthN-modulen för att autentisera användaren på MVPD IdP. |
| \[Valfritt\] AuthN-enhet | AuthN-app | Om direktuppspelningsenheten inte har någon användaragent (t.ex. webbläsare) är AuthN-programmet ett webbprogram för programmerare som nås från en separat användares enhet via en webbläsare.  |
| Adobe infrastruktur | Adobe Pass Service | En tjänst som integreras med MVPD IdP- och AuthZ-tjänsten och som ger autentiserings- och auktoriseringsbeslut. |
| MVPD-infrastruktur | MVPD IdP | En MVPD-slutpunkt som tillhandahåller autentiseringsbaserad autentisering för att validera användarens identitet. |
|  | MVPD AuthZ-tjänst | En MVPD-slutpunkt som ger auktoriseringsbeslut baserat på användarens prenumerationer, föräldrakontroll osv. |

 

Ytterligare termer som används i flödet definieras i [Ordlista](http://tve.helpdocsonline.com/adobe-pass-glossary).

## Flöden{#flows}

### Dynamic Client Registration (DCR)

Adobe Pass använder DCR för att säkra klientkommunikationen mellan ett programmeringsprogram eller en server och Adobe Pass tjänster. DCR-flödet är separat, beroende och nödvändigt och finns här: http://tve.helpdocsonline.com/dynamic-client-registration


### Appflöden för direktuppspelning (smart enhet)

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/clientless_1st_screen_updated.PNG)

 

#### Startflöde

1. Ditt program startas och det inledande användargränssnittet läses in.

2. Hämta/generera ett enhets-ID.

3. Utfärda ett Check-authentication-anrop för att se om enheten redan är autentiserad.  Exempel: [`<SP_FQDN>/api/v1/checkauthn [device ID]`](/help/authentication/check-authentication-token.md)

4. Om `checkauthn` samtalet lyckades, fortsätt till auktoriseringsflödet från och med steg 2.  Starta registreringsflödet om det inte fungerar.

 

#### Registreringsflöde

1. Skaffa en registreringskod och URL som användaren kan använda för att få åtkomst till inloggningsappen för den andra skärmen och visa dessa för användaren:

   a. Skicka en begäran om POST till Adobe Registration Code Service och skicka ett hash-kodat enhets-ID och en &quot;Registration URL&quot;.  Exempel: [`<REGGIE_FQDN>/reggie/v1/[requestorId]/regcode [device ID]`](/help/authentication/registration-code-request.md)

   b. Ange den returnerade registreringskoden och URL-adressen till användaren.

   c. Instruera användaren att växla till en webbkompatibel enhet, navigera till URL:en och ange sedan registreringskoden.

 

#### Auktoriseringsflöde

1. Användaren återgår från den andra skärmappen och trycker på knappen &quot;Fortsätt&quot; på enheten. Du kan också implementera en avsökningsmekanism för att kontrollera autentiseringsstatusen, men Adobe Primetime-autentiseringen rekommenderar att du använder knappmetoden Fortsätt framför avsökningen. <!--(For information on employing a "Continue" button versus polling the Adobe Primetime authentication backend server, see the Clientless Technical Overview: Managing 2nd-Screen Workflow Transition.)--> Till exempel: [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md)

2. Skicka en GET-förfrågan till Adobe Primetime autentiseringsauktoriseringstjänst för att initiera auktorisering. Exempel: `<SP_FQDN>/api/v1/authorize [device ID, Requestor ID, Resource ID]`

<!-- end list -->

- Om svaret anger att åtgärden lyckades: Användaren har en giltig AuthN-token OCH användaren har behörighet att titta på det begärda mediet (det finns en giltig AuthZ-token för den här användaren).

- Om svaret indikerar fel: Undersök det undantag som genereras för att avgöra dess typ (AuthN, AuthZ eller något annat):

   - Om det var ett AuthN-fel startar du om registreringsflödet.

   - Om det var ett AuthZ-fel har användaren inte behörighet att titta på det begärda mediet och någon typ av felmeddelande ska visas för användaren.

   - Om det finns något annat fel (anslutningsfel, nätverksfel osv.) visar sedan ett felmeddelande för användaren.

 

#### Visa medieflöde

1. Presentera mediealternativ. Användaren väljer de media som ska visas.

2. Är mediet skyddat?

   a. Din app kontrollerar om mediet är skyddat.

   b. Om mediet är skyddat startar din app autentiseringsflödet (AuthZ) ovan.

   c. Om mediet inte är skyddat kan du spela upp mediet för användaren.

3. Spela upp mediet.


### Appflöde för AuthN (andra skärmen)

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/smart_dev_second_flow.png)

1. Hämta en lista över MVPD för den här användaren. Exempel: [`<SP_FQDN>/api/v1/config/[requestorID]`](/help/authentication/provide-mvpd-list.md)

1. Initiera autentiseringsflödet.  Exempel: [`<SP_FQDN>/api/v1/authenticate [requestorID, MVPD ID, Redirect URL, Domain name, Registration Code, "noflash=true"]`](/help/authentication/initiate-authentication.md)

1. Kontrollera om autentiseringen lyckades.  Exempel: [`<SP_FQDN>/api/v1/checkauthn/[registration code][requestor ID]`](/help/authentication/check-authentication-token.md)

1. Skicka tillbaka användaren till din Smart Device-app för att slutföra auktoriseringsflödet.

 

## Plattforms-SSO {#platform-sso}

Vissa plattformar har dedikerat stöd för enkel inloggning (SSO). Implementeringsinformation finns för varje plattform:

- [Apple SSO](http://tve.helpdocsonline.com/rest-api-apple-sso)
- Amazon SSO

## TempPass och Promotional TempPass för REST API {#temppass}

För TempPass- och Promotional TempPass-implementeringar där användaren inte behöver ange inloggningsuppgifter kan autentisering implementeras direkt i Streaming App. 

**För att kunna använda detta API måste strömningsappen se till att enhets-ID är unikt eftersom detta används för att identifiera token, tillsammans med de valfria extra data.**


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/Free%20preview%20option.png?dc=201612071020-0)

### Relaterad information {#related}

- [REST API-referens](/help/authentication/rest-api-reference.md)
