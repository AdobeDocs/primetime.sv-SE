---
title: MVPD-integreringsfunktioner
description: MVPD-integreringsfunktioner
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1704'
ht-degree: 2%

---

# MVPD-integreringsfunktioner

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Ökning {#mvpd-int-features-overview}

Adobe Primetime autentisering stöder de nya standarderna för TV Everywhere. Det är kompatibelt med **CableLabs OLCA-specifikation (Online Content Access)**, som innehåller tekniska krav och arkitektur för leverans av video till en Pay TV-kund från onlinekällor. Adobe deltog i det gemensamma CableLabs-projektet för interopt-testning i juni 2011 och klarade testprocessen för en implementering av en tjänsteleverantör.  Adobe är även aktiv medlem i **OATC (Open Authentication Technical Consortium)** och deltar i flera av underkommittéernas projekt för att utarbeta specifikationer som en del av det organet.

Efter att ha beskrivit efterlevnad av OLCA för autentisering i Primetime och Adobe deltar i OATC, är det också viktigt att notera att Primetime-autentisering i själva verket är&quot;protokollagnostisk&quot;.  Men i det här skedet av TVE-eran är Primetime-autentiseringen helt klart inriktad på OLCA-standarderna.  Standarderna beskriver för närvarande överenskomna sätt för de olika TVE-spelarna (programmerare, programmerare och tjänsteleverantörer) att implementera TVE-funktioner. Många av dessa funktioner listas i tabellerna nedan, med länkar till relaterade sidor som innehåller detaljer och exempel på hur funktionerna ska implementeras.

Informationen i tabellerna är avsedd att driva integreringsprocessen för autentisering av Primetime mot enhetlig funktionalitet i alla MVPD-integreringar. I prioriteringskolumnen rangordnas funktionerna i A, B och C:

* S - Dessa måste ha funktioner för den första utrullningen av en integrering.
* B - Detta är viktiga förbättringar av den inledande integreringen som ska läggas till efter den första utrullningen.
* C - Detta är ytterligare förbättringar av integreringen som kan implementeras efter B-kraven.


## 1. De viktigaste funktionerna {#core-func-features}


| Nej. | Funktion | Beskrivning | Prioritet | Anteckningar |
|------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1.1 | [Programmerarinitierad inloggning](/help/authentication/authn-oauth2-protocol.md) | Visningsprogrammet väljer MVPD och initierar autentiseringsflödet (AuthN) från programmeringsmärkets webbplats eller tillämpning. | A+ |                                                                                                                                                         |
| 1.2 | [Kanalbaserad autentisering](/help/authentication/authz-usecase.md) | När den har autentiserats kan auktoriseringen (AuthZ) ske i bakgrunden, med bara en nätverkskanal-ID och en användaridentifierare skickas till MVPD. | A+ |                                                                                                                                                         |
| 1.3 | UserID-beständighet | MVPD tillhandahåller ett okomplicerat, beständigt användar-ID. | A |                                                                                                                                                         |
| 1.4 | [Stöd för enkel inloggning](/help/authentication/sso-support.md) | Visningsprogrammet loggar in med MVPD på webbplatsen för ett varumärke och kan sedan gå till ett annat varumärke och inte uppmanas att logga in igen. AuthN-sessionen delas mellan varumärkena. SSO-stöd gäller både webbplatser och mobilapplikationer/enhetsapplikationer.  För MVPD-program krävs att antingen ett användar-ID eller någon annan användartoken som kan användas för AuthZ för olika varumärken returneras. | A |                                                                                                                                                         |
| 1.5 | Enhetsoptimerad användarupplevelse vid inloggning (UX) | MVPD har stöd för att ändra storlek på inloggningsskärmen så att den passar dimensionerna för den enhet som vyn använder. | A |                                                                                                                                                         |
| 1.6 | Standardlogotyp för MVPD-väljare | MVPD tillhandahåller en URL till en standardlogotyp med lämpliga dimensioner (112x33 pixlar). | A | Logotypen ska skötas av MVPD och ska cachas av CDN. |
| 1.7 | [Tjänstleverantörsomfång](/help/authentication/serv-provider-scoping.md) | MVPD stöder överföring av varumärkesidentifieraren (Requestor value) i AuthN-begäran. | A- | Detta aktiverar en tjänsteleverantörsspecifik inloggningsfunktion. |
| 1.8 | [Auktorisering för flera kanaler](/help/authentication/mvpd-preflight-authz.md#preflight-multich-authz) | MVPD stöder en programmerare som skickar flera kanaler i en enda auktoriseringsbegäran. | B+ |                                                                                                                                                         |
| 1.9 | iFrame- eller JS Pop-up-baserad autentisering | Programmeraren kan integrera inloggningsflödet i en iFrame- eller popup-upplevelse i stället för en HTTP-omdirigering. | B |                                                                                                                                                         |
| 1.10 | [Programmerarinitierad utloggning](/help/authentication/usecase-mvpd-logout.md) | Visningsprogrammet har en autentiserad session både på Programmerarens webbplats eller i appen och med MVPD. Visningsprogrammet kan initiera en federerad utloggning från programmerarens webbplats och utloggningen rensar även sessionen på MVPD-portalen. | B | Ser till att delade datorer skyddas mot missbruk ur programmeringsperspektivet. |
| 1.11 | [Felmeddelanden för anpassad auktorisering](/help/authentication/error-reporting.md) | MVPD skickar en egen felsträng, vilket är lämpligt för programmerarens externa webbplats eller app att visa för användaren. | B | Aktiverar merförsäljningsscenarier |
| 1.12 | **Användarmetadata för autentiseringssvar** | MVPD AuthN-svaret kan innehålla användarmetadata som fungerar som tips för personalisering av användarens upplevelse under tillståndsflödet. Detta krav möjliggör tips om föräldrakontroll från MVPD till programmeraren. | B- |                                                                                                                                                         |
| 1.13 | MVPD-initierad autentisering | Visningsprogrammet slutför en AuthN-session på MVPD-portalen och navigerar sedan till programmerarens TVE-webbplats. Användaren uppmanas inte att ange MVPD-väljaren och autentiseras automatiskt. | B- |                                                                                                                                                         |
| 1.14 | UserID-omfång | MVPD-användar-ID:t ska finnas i två former - en som omfattar programmerare och den andra som omfattar hela Adobe för bedrägeri.  På så sätt kan Adobe dela programmeringsomfångets MVPD-användar-ID utan ytterligare kryptering eller krånglighet. | C |                                                                                                                                                         |
| 1.15 | Tillgångsbaserad auktorisering | När AuthN har slutförts kan AuthZ inträffa i bakgrunden genom att skicka strukturerade data som kan innehålla nätverk, bildspel, resurser, klassificeringar av föräldrakontroll och mycket mer efter behov. Detta aktiverar föräldrakontroll för alla AuthZ-anrop från Programmer till MVPD. | C |                                                                                                                                                         |
| 1.16 | MVPD-initierad utloggning | Visningsprogrammet har en autentiserad session både på Programmerarens webbplats eller i dess app och med MVPD. Visningsprogrammet kan initiera en federerad utloggning från MVPD:s webbplats som även rensar sessionen på alla externa programmerarwebbplatser. | C |                                                                                                                                                         |
| 1.17 | Auktoriseringsskyldigheter | MVPD ger ytterligare villkor i AuthZ-svaret, till exempel loggning, eller en uppdaterad OLCA (maximum parent control rating). | C |                                                                                                                                                         |
| 1.18 | IP-adresskontext | MVPD kräver att IP-adressen skickas explicit. För AuthZ, där anropen är på serversidan, ger detta information om MVPD-bedrägerispårning om var användaren kommer från på AuthZ-anropet. | C |                                                                                                                                                         |
| 1.19 | TTL-värde (Token Persistence Time-to-live) dynamiskt definierat | MVPD kan ställa in TTL för Primetimes autentiseringstoken dynamiskt via egenskaper i svaret, så att Adobe är utanför slingan för TTL-ändringar. | C- |                                                                                                                                                         |
| 1.20 | Enhetstyp | MVPD stöder överföring av enhetstypen i AuthN- eller AuthZ-begäran. Den här egenskapen informerar MVPD om vilken typ av enhet som innehållet ska förbrukas på, så att de kan justera TTL för AuthN- eller AuthZ-token så att den överensstämmer med enhetens egna säkerhetsöverväganden. | C- | Detta är användbart för den klientlösa plattformen, där det kan vara svårt att visa varje enhetstyp som en konfigurationsinställning på autentiseringssidan Primetime. |



## 2. Funktioner {#operational-features}

| Nej | Funktion | Beskrivning | Prioritet | Anteckningar |
|-----|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|-------|
| 2.1 | Drifttid dygnet runt | Ett MVPD-avtal som ska användas dygnet runt och mäta mot det över tiden. | A |       |
| 2.2 | Testa autentiseringsuppgifter för varje programmerare | MVPD tillhandahåller separata testkonton för varje programmerare. | A |       |
| 2.3 | Schemaläggning för förfallodatum och förnyelse av certifikat | En MVPD-dokumenterad plan med ett schema för att säkerställa att SAML-certifikat är aktuella. | A- |       |
| 2.4 | Genomsnittlig svarstid under 250 ms/svar | Ett MVPD-avtal för att eftersträva låg latens och mäta mot det med tiden. | A- |       |
| 2.5 | Hosting Own MVPD Picker Logo | MVPD måste ha sin egen logotyp och den ska skyddas av CDN-cache. | B |       |
| 2.6 | Supportavtal för eskalering | En plan som dokumenterats av MVPD för eskalering och som hålls uppdaterad och granskas minst en gång i kvartalet. | A |       |
| 2.7 | Utgångsskydd | En plan för ett multifunktionsskyddat skyddsprogram tillsammans med Adobe om nedbrytningsåtgärder som kan användas generellt vid behov. | B |       |
| 2.8 | Underhåll separata mellanlagrings- och produktionsslutpunkter | Ett MVPD-integrationstest som inte kräver värdfilsförfalskning för att testa mellanlagringsintegreringen. | B |       |
| 2.9 | Ytterligare QA-slutpunkt | MVPD har en ytterligare QA IdP-integrering för utveckling av gemensamma nya funktioner.  Om vi stöttar detta blir det mindre troligt att vi behöver UAT-specialförfrågningar för testning av appbutikscertifikat. | C |       |





## 3. Autentiseringsupplevelsefunktioner {#authn-exp-features}


| Nej | Funktion | Beskrivning | Prioritet | Anteckningar |
|-----|----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| 3.1 | Autentiseringskonvertering över minimal förväntning | MVPD säkerställer en lägsta konverteringsgrad som ger belägg för att funktionen är tillräcklig (5 %) och rimlig (30 %). | A |                                                                                                                                                           |
| 3.2 | Inline lösenordsåterställning | Med MVPD kan du återställa lösenord som är infogade i det federerade AuthN-flödet. | A |                                                                                                                                                           |
| 3.3 | Registrering av infogat konto | MVPD ger ett sätt att skapa ett nytt kontoinfogat till ett federerat AuthN-flöde. | A |                                                                                                                                                           |
| 3.4 | Onlinehjälp/support | MVPD tillhandahåller ett hjälpmedel som kan användas under det federerade AuthN-flödet. | A |                                                                                                                                                           |
| 3.5 | Modembaserad autentisering hemma | MVPD autentiserar automatiskt en enhet när den finns i det lokala nätverket för en registrerad modell (endast ISP MVPD). | B | Det här är en lägre prioritet eftersom det är en optimering som många ännu inte kan stödja och som ger upphov till vissa problem när det gäller begränsning av bedrägerier och föräldrakontroll |
Nu kan du importera kod från markeringstabellen direkt med dialogrutan Arkiv/Klistra in tabelldata...



## 4. Analysfunktioner {#analytics-features}


| Nej | Funktion | Beskrivning | Prioritet |
|-----|--------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| 4.1 | Justering av autentiseringskonverteringsfunktion | MVPD har ett mätvärde för AuthN-begäranden som börjar med SAML AuthN-begäran - som justeras mot parametrarna för Primetime-autentisering och programmerarens AuthN-begäran. | A |
| 4.2 | Unika användare | Användare som har autentiserats och deduplicerats i en månadsvis uppdatering över flera dagar. | A |
| 4.3 | Tidszonsredovisning | Rapporterna innehåller tidszon för när dagen ändras. | A |





## 5. Funktioner för att minska bedrägerier {#fraud-mitgn-features}


| Nej | Funktion | Beskrivning | Prioritet | Anteckningar |
|-----|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------|
| 5.1 | Validering av videoprenumerant vid autentisering | MVPD säkerställer att användaren är en giltig videoprenumerant under AuthN-flödet. | A |                                                                                                |
| 5.2 | Hastighetsbegränsning för autentisering/auktorisering | MVPD har stöd för begränsning av användningen av webbtjänster för att vid behov begränsa användningen från ett visst användarkonto. | B |                                                                                                |
| 5.3 | Beständigt användar-ID med globalt omfång för Adobe | MVPD säkerställer att Adobe har ett användar-ID som kan spåras mellan programmerare för att upptäcka bedrägeri. Detta behöver inte tillhandahållas kunden direkt. | B | Online Multimedia Authorization Protocol (OMAP) Specification and Real User Monitoring (RUM). |
| 5.4 | Validering av samtidig användning | MVPD har ett sätt att spåra och begränsa den samtidiga användningen av prenumerantkontot utöver ett affärströskelvärde. | B |                                                                                                |

## P1. Proxyspecifika funktioner {#proxy-sp-func-features}

| Nej | Beskrivning | Prioritet | Anteckningar |
|-------|--------------------------------------------------------------------------------|----------|---------------------------------------------------|
| P 1.1 | Proxy som ansvarar för att uppdatera listan över undergruppsdokument är korrekt | A |                                                   |
| P 1.2 | Proxy levererar en logotyp i lämplig storlek för varje subMVPD | A | Vissa live-subMVPD-program har inte rätt logotypstorlek |
| P 1.3 | Proxy levererar rätt profilerad inloggningssida för varje subMVPD | A |                                                   |
| P 1.4 | Proxy som är ansvarig för specifika tjänsteleverantörsnamn med subMVPD-lista | B |                                                   |
| P 1.5 | Proxy anger alla subMVPD-egenskaper korrekt (iFrame-storlek, TTL, logotyp etc) | A |                                                   |
| P 1.6 | Proxy anger ett separat enhets-ID | B |                                                   |

## P2. Proxyfunktioner {#proxy-op-features}

| Nej | Beskrivning | Prioritet |
|-------|----------------------------------------------------------------------------------------|----------|
| P 2.1 | API-nyckeln är skyddad | A |
| P 2.2 | Testa autentiseringsuppgifter för den första subMVPD som används i direktintegrering för varje ny begäran | A |
| P 2.3 | subMVPD-listor är korrekta och fullständiga per beställare | A |
