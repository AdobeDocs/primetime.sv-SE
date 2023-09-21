---
title: Användningsexempel för programmerare
description: Användningsexempel för programmerare
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 0%

---

# Användningsexempel för programmerare {#programmer-use-cases}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Ökning {#overview}

I det här dokumentet sammanfattas de fall där programmeringsintegrering används som stöds av Adobe Primetime-autentisering. Du kan kontrollera den här sidan innan du påbörjar ett integreringsprojekt för att se vilka funktioner som för närvarande stöds.

## Användningsexempel {#use-cases}


### Grundläggande integrering: Samlad autentisering och auktorisering för ett enda kanalnätverk {#basic-integration}

**Prioritet** - Hög

**Uppdelning** - En app för TV-reklam med en enda programmerare med 1 Channel Network som värd inuti upplevelsen

Detta gör att programmerare kan erbjuda premiuminnehåll, i sin egen profilerade TVE-app*, med en federerad behörighetskontroll till MVPD. RequestID ska justeras så att det matchar varumärket för det program som betjänar innehållet med visningsprogrammet. I det här scenariot finns det en 1 till 1-relation mellan Adobe Primetime-autentiseringsbegärande-ID och det resurs-ID som verifieras för berättigande.

>[!NOTE]
>
>TVE-appen används i det här dokumentet för att tillsammans referera till olika typer av program (webbappar, mobilappar osv.) stöds av Adobe Primetime-autentisering. Kolumnen Plattformar nedan kan innehålla information om vilka plattformar som stöds för olika användningsområden.

#### Specifika användningsfall (gäller de flesta integreringar) {#sp-use-cases-basic-int}

| Prioritet | Användningsfall | Beskrivning | Plattformar | MVPD-anteckningar |
|:--------:|:-----------------------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------:|:-----------------------------------------:|
| Hög | MVPD Discovery from Programmer TVE App | Användaren startar i programmerarens profilerade TVE-app och uppmanas att välja sin MVPD-leverantör. | Webb (SWF/JS) Mobile (iOS/Android), klientlöst API (för sekundär skärm) |                                           |
| Hög | Federated Authentication från programmerarens TVE-app | Användaren startar i programmerarens varumärkesprofilerade TVE-app och när användaren har valt sin MVPD-leverantör, överförs användaren till MVPD:s egen inloggningssida för att ange sina inloggningsuppgifter. | Webb (SWF/JS) Mobile (iOS/Android) |                                           |
| Hög | Auktorisering från programmerarens TVE-app | När användaren har autentiserats kan programmerarens TVE-app göra återkanalsauktoriseringsbegäranden till MVPD för att kontrollera användarens berättigande. Vanligtvis kontrollerar detta bara om kanalnätverket finns i användarens MVPD-prenumerationspaket.                                  I det här fallet kommer begärande-ID och resurs-ID att matcha 1:1. | Alla plattformar |                                           |
| Medel | Logga ut från programmerarens TVE-app | Gör det möjligt för användaren att logga ut och rensa Adobe Primetime AuthN/AuthZ-tokens för autentisering. I många fall loggar detta även ut användaren från MVPD. MVPD:er varierar dock om detta stöds eller inte. Den rensar alltid Adobe Primetime autentiseringssession och token. | Alla plattformar utom XBox Native | Flera MVPD-program stöder inte detta. |
| Hög | Enkel inloggning på webbplatser och appar | Låter användaren dela inloggningssessionen mellan webbplatser och appar utan att behöva logga in igen. | Alla plattformar utom klientlöst API | Kräver minst SDK 1.7 för vissa MVPD-program. |

### En TVE-app som är värd för flera kanalnätverk {#single-app-multi-channel}

**Prioritet**- Hög

Gör att programmeraren kan samla flera kanalnätverk med innehåll på samma varumärkesskyddade mål för sina tittare.

#### Specifika användningsfall {#sp-use-cases-singl-tve-app}

| Prioritet | Användningsfall | Beskrivning | Plattformar | MVPD-anteckningar |
|--------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Hög | Distinkt kanalauktorisering | Användaren kan se innehåll från flera kanalnätverk i samma TVE-app. Programmeraren kan ringa auktoriseringsanrop som är specifika för varje kanalnätverk för att bekräfta användarens behörighet. | Alla plattformar | Alla MVPD-program har nu stöd för detta i någon form. |
| Låg | Fråga om preflight-auktorisering | Detta gör att programmeraren kan kontrollera vilka kanaler användaren har i sitt paket i ett enda API-anrop. Detta görs innan faktiska AuthZ-anrop för att filtrera innehåll från användargränssnittet som användaren inte har tillgång till. |               | De flesta programmeringsgränssnitten visar inte dessa data som användarattribut än, så Adobe gör i själva verket AuthZ-anrop för att hämta dem. De flesta programmeringsgränssnitten är dessutom begränsade till 5 i taget, eftersom de inte har stöd för flera kanaler i ett enda anrop.                             Det är viktigt att kontrollera hur många kanaler programmeraren behöver för att utföra preflight-kontroller. Oavsett vilket nummer det är, måste vi kontrollera att det är ok med MVPD. De flesta programmeringsgränssnitten har för närvarande inte stöd för fler än fem kanaler (3 kvartal 2013). |

### Tillgångsnivåauktorisering {#asset-level-authz}

**Prioritet** - Låg

**Uppdelning** - Skicka en tillgångsidentifierare vid auktoriseringsbegäran

**Plattformar** - Alla plattformar

#### Specifika användningsfall {#sp-use-cases-asset-lvl-authz}

Gör att MVPD kan hämta tillgångsnivåanalyser för varje AuthZ-anrop. Nackdelen med detta är att AuthZ-cachen för Adobe Primetime-autentisering negeras.

| Prioritet | Användningsfall | Beskrivning | Plattformar | MVPD-anteckningar |
|--------|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------------|--------------------------------------|
| Låg | Skicka en tillgångsidentifierare vid auktoriseringsbegäran | Gör att MVPD kan hämta tillgångsnivåanalyser för varje AuthZ-anrop.  Nackdelen med negering av Adobe Primetime-autentiseringscache för AuthZ. | Alla plattformar | Endast en MVPD stöder detta för närvarande. |




### Föräldrakontroll {#parental-controls}

**Prioritet** - Låg

Gör att begränsningar för MVPD-användarkonton kan tillämpas på programmerarens TVE-app.

| Prioritet | Användningsfall | Beskrivning | Plattformar | MVPD-anteckningar |
|--------|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|-----------------------------------|
| Låg | Filtrera innehåll baserat på användarattribut | Gör det möjligt för programmeraren att kontrollera högsta tillåtna klassificering för en användare innan listan över tillgängligt innehåll återges för användaren. | Webb (Flash/JS) Mobile (iOS/Android) | Fungerar endast med ett MVPD för närvarande. |
| Låg | Godkänn innehållsklassificeringar i AuthZ-begäran | Gör att programmeraren kan skicka den specifika klassificeringen av innehållet som användaren vill se som en del av AuthZ-begäran till MVPD relaterat till #3, eftersom klassificeringar vanligtvis finns på tillgångsnivå. | Alla plattformar | Fungerar endast med ett MVPD för närvarande. |

#### Anpassning av MVPD-integrering per programmeringsmärke {#mvpd-int-cust-prog-brand}

**Prioritet** - Medel

Aktiverar anpassad upplevelse under AuthN- eller AuthZ-felmeddelanden.

| Prioritet | Användningsfall | Beskrivning | Plattformar | MVPD-anteckningar |
|--------|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------------------------------------|
| Medel | Identifierare för tjänstleverantör i AuthN-begäran. | Aktivera specifik branding på inloggningssidan för MVPD som är specifik för tjänsteleverantören. Aktivera även automatiskt val av standardinställning för att matcha målgruppen, t.ex. Spanska för Univision. | Alla plattformar | Varierar med MVPD. Vissa stöder inte detta. |
| Medel | Anpassade felmeddelanden i AuthZ-svar | Aktiverar programmerings- eller varumärkesspecifika felmeddelanden från MVPD som kan innehålla ett specifikt meddelande om merförsäljning med en länk som uppgraderar paketet. | Webb, Android, iOS | Varierar med MVPD. Vissa stöder inte detta. |


### Användningsexempel för anslutna enheter {#connected-devices}

| Prioritet | Användningsfall | Beskrivning | Plattformar | MVPD-anteckningar |
|--------|-------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Medel | XBox LiveID SSO mellan appar och konsoler | Låter användaren dela AuthN-session mellan appar och mellan olika spelkonsoler - som är kopplade till deras LiveID-konto. | XBox Native SDK | De flesta MVPD-program gillar inte detta eftersom den vanliga modellen är att binda token till enheten - inte till användaren.                             Vi rekommenderar inte det här tillvägagångssättet längre om det går. |
| Hög | Ansluten enhet med token bundna till appID på enheten | Gör att programmeraren kan binda MVPD-berättigandet i token till appID på den enhet som det utfärdades till. | Klientlöst API | Den anslutna enheten justeras närmare standardimplementeringen för tokens.                             Behöver fortfarande förbättras för att vara ett enhetstäckande ID. |

### Enhetsspecifik längd för AuthN TTL {#authn-ttl-length}

Aktivera TVE-berättigande för specialhändelser som kanske inte finns i MVPD-tillståndsdatabasen, som vanliga kanaler.

| Prioritet | Användningsfall | Beskrivning | Plattformar | MVPD-anteckningar |
|--------|------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|--------------------------------------------------------------------------------------------------------------------------|
| Hög | Ange olika TTL-värden per plattform | Gör att programmeraren kan skapa en annan TTL-längd för webb, mobiler och anslutna enheter. För närvarande stöder Adobe Primetime-autentisering möjligheten att ha tre separata TTL-värden: Webb (Flash) Mobile/HTML5 Client less - Connected Devices |           | Vissa MVPD-program ställer in TTL dynamiskt. Adobe kan vid behov åsidosätta dessa dynamiska inställningar med hjälp av konfigurationsinställningarna. |

### Särskilda händelsebaserade program {#special-event}

**Prioritet** - Låg

Aktivera TVE-berättigande för specialhändelser som kanske inte finns i MVPD-tillståndsdatabasen, som vanliga kanaler.

| Prioritet | Användningsfall | Beskrivning | Plattformar | MVPD-anteckningar |
|--------|---------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|------------------------------------------|
| Låg | Flera kanaler som proxy för en händelse | Detta gjordes för OS, där abonnenten behövde två olika kanaler i sitt paket för att få tillgång till dem. I det här fallet skapade Adobe Primetime-autentiseringen ett nytt resurs-ID och hade alla programmeringsskyltar att mappa till de specifika kanalerna i sin tur.  Det där fungerade bra med tillräckligt med avancerad avisering. Det här var viktigt eftersom de flesta programmeringsgränssnitten inte stöder flera resursanrop. | Alla plattformar | Stöds av alla videofilmare med god varsel. |
| Låg | Särskilt nytt händelseprogram, använda befintliga kanalresurser | Det här gjordes för Mars Madness. Innehållsleverantören skapade ett nytt program med ett nytt requestID. Alla MVPD-program behövde stöd för det nya beställar-ID:t i deras system. Resurs-ID:n var normala kanaler.  En del programmeringsdokument behövde också mappa kanalerna som giltiga enligt den nya begäraren, så mer tid behövdes för dessa fall. | Alla plattformar | Stöds av alla videofilmare med god varsel. |
| Låg | Befintligt beställar-ID, resurs-ID | Det här gjordes för mästarens golfhelgsturnering. Det var bara ett litet event under ett par dagar, och mallarna hade en egen mobilapp som kunde visa innehållet. Programmeraren planerade att betala för Adobe Primetime-autentiseringstrafiken och bara använda sitt standardprogram för beställar-ID och resurs-ID. Det enda tricket var att programmeraren delade ett mobilcertifikat för beställar-ID-signering med mallarna och att lägga till det i konfigurationen som deras säkerhetskopieringscertifikat för den helgen. | Alla plattformar | Ingen påverkan för programmeringsdokumentskydd |

### Integrering med innehållsserver {#content-server-integration}

**Prioritet**- Medel

Aktivera validering av medietoken innan videoströmmen släpps till klientspelaren.
| Prioritet | Användningsfall | Beskrivning | Plattformar | MVPD-anteckningar | |—|—|—|—|—|—| | Hög | Programmer Federated Player - med behörighet på sidnivå | Adobe Primetime autentiserings-API:er görs i JavaScript på sidan och token skickas till spelaren. Token kan skickas till valideringstjänsten på ett par sätt: Hämta param på URL-parametern för verifieringstjänsten som skickas i frågesträngen för API:t för det externa gränssnittet i flödet | | | | Medel | Programmer Federated Player - med intern spelarbehörighet | Adobe Primetime autentiserings-API:er görs i ActionScriptet i spelaren SWF, så token är tillgänglig för spelaren från återanropet.                                                                                                                                                                                         | | | | Hög | Syndikerad spelare - finns på MVPD Portal med sidnivåautentisering Använda en iFrame för att lägga in spelaren | Liknar spelaren med sidnivåauktorisering, men med spelarsidomslutningen iFramed i MVPD-portalen. Autentisering måste ske separat i MVPD-portalen.                                                                                                                                                    |           |                        |


<!--
>[!RELATEDINFORMATION]
>
>* MVPD Integration Features
>* Entitlement Flow
>* Platform / Device Requirements
-->
