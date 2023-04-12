---
title: REST API - översikt
description: Översikt över övriga API:er
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1596'
ht-degree: 0%

---


# REST API - översikt {#rest-api-overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.


## Översikt {#over}

Adobe Primetime REST API för autentisering ger direktåtkomst till TVE-autentiserings- och auktoriseringstjänsterna (TV Everywhere). Detta API har stöd för två primära arkitekturer: Server-till-server eller anslutna enheter (t.ex. spelkonsoler, smarta TV-apparater, digitalboxar etc.) program som inte har webbläsarfunktioner. 

 

### Server-till-server

Server-till-server-lösningar omfattar program för programmeringsklienter som integreras med programmeringstjänster som ansluter till Adobe Primetime autentiseringstjänster för TVE-flöden. Detta arbetssätt flyttar de flesta TVE-implementeringar från klienten till servern där en enda, enhetlig autentiseringsmodul kan skapas och underhållas. Klientprogrammets primära återstående ansvar är hanteringen av en webbvy för användarautentisering.

 

### Anslutna enheter

Appar för anslutna enheter kommunicerar direkt med Primetime Authentication via REST API:er för att utföra konfigurations-, registrerings-, autentiseringsstatuskontroller och auktoriseringsflöden, medan en andra skärmapp (webbläsarapp) krävs för autentiseringsflödet. Inbyggda SDK:er används därför inte.

 

### Övriga arkitekturer

Förutom de två primära REST API-baserade arkitekturerna, server-till-server- och Direct-klientlösningarna för smarta enheter, finns det andra arkitekturer.  Den främsta av dem är SDK-arkitekturen, som använder en klientkomponent som kallas åtkomstaktivering och som Primetime-autentisering tillhandahåller programmerare.  Appen använder API:er för åtkomstaktivering för att hantera start, autentisering, auktorisering och utloggning.  All kommunikation mellan programmerarens app och Primetimes autentiseringsservrar sker via Access Enabler.  En annan variant av Access Enabler finns för följande plattformar: JavaScript, iOS, tvOS, Android och FireTV.

Även om det är möjligt att använda REST API direkt på klientplattformar som stöder systemspecifika SDK:er utanför en Server-to-Server-lösning, rekommenderas inte detta.

 

## REST API-proffs och Cons {#ProsAndCons}

Adobe Primetime Authentication REST API skapades för att tillhandahålla en TV Everywhere-lösning (TVE) för enheter som inte har webbläsarfunktioner eller beständig lagring. REST API har stöd för alla autentiserings- och auktoriseringsflöden, men eftersom det saknas en systemspecifik SDK-komponent. De SDK:er som tillhandahålls och underhålls av Adobe Primetime Authentication har färdiga funktioner som implementerar affärsregler som måste implementeras och underhållas av programmerarna i händelse av REST API. I tabellen nedan beskriver vi de begränsningar i REST API som programmerare måste ta itu med.

 

### Server-till-server jämfört med klientbaserade proffs och kontors

En Server-till-Server-arkitektur är ett sätt att konsolidera merparten av den autentiserings- och auktoriseringsrelaterade logiken i en enda logisk enhet eller implementering.  Det här tillvägagångssättet har fördelar och nackdelar.  Yrkesverksamma inom följande områden:

* En enda implementering för autentisering och auktorisering av affärslogik.
* Undvik behovet av att implementera logiken på alla plattformar som stöds med plattformens inbyggda verktyg.
* Möjlighet att uppdatera funktioner utan att behöva uppdatera klienter med alla tillhörande krav (t.ex. uppdateringar av appbutiker).
* **Enklare** utöka och anpassa funktionerna för authN och authZ (t.ex. lägg till D2C).
* Direkt hantering av tillhörande trafik för bättre kontroll, kvalitet och övervakning.

 

Även här anges konerna i programmerarens ansvarsområden, men omfattar följande:

* SSO måste implementeras för varje klient för plattformar utan enkel inloggning (Platform SSO).
* Programmerarna måste vid behov implementera MVPD-specifik logik.
* Alla plattformar som använder REST API delar en enda konfiguration som styr egenskaper som till exempel autentiserings-TTL:er.

 

### Anslutna enheter

För de flesta anslutna enheter måste REST API användas på ett eller annat sätt eftersom en SDK inte är tillgänglig. Den anslutna enheten använder antingen REST API direkt eller integreras med en Server-till-Server-lösning som använder REST API.

## Programmerarnas ansvar {#programmer-responsibilities}

Följande gäller för både Server-to-Server- och Connected Device-program.

| **Funktionalitet** | **Ansvarig för hantering av funktionaliteten** | **Beskrivning av begränsningarna i det aktuella klientlösa API:t och skillnader från systemspecifika SDK:er** |
| --- | --- | --- |
| Konfigurationsinställningar som används per plattform | Adobe | Ett **större begränsning** om att använda REST API på alla plattformar (inklusive mobila enheter som iOS &amp; Android) är att de konfigurationsinställningar som motsvarar REST API i vårt konfigurationsverktyg för TVE Dashboard tillämpas på alla enheter (även om det finns en iOS-enhet som kör ett systemspecifikt program som implementerats ovanpå vårt REST API). Denna begränsning **kan brytas** de överenskomna TTL:erna och de överenskomna plattformsinställningarna med de godkända PDF:erna - om dessa skiljer sig åt för varje plattform. [1](#1) |
| Enkel inloggning | Programmerare | Med REST API är enkel inloggning bara tillgängligt på plattformar som stöder enkel inloggning (t.ex. Apple, Roku, Amazon) medan enkel inloggning inte kan garanteras för andra plattformar när REST API används. SDK:erna cachelagrar data på en webbplats/i en app. Det innebär att användaren loggar in en gång på en webbplats/app och redan är inloggad på deltagande webbplatser, utan att någon användarinteraktion behövs. [2](#2) |
| Enkel utloggning | Programmerare | I ett systemspecifikt SDK SSO-scenario kommer utloggning från ett deltagande program att logga ut användaren oavsett var användaren befinner sig. På den aktuella REST API:n som vi inte stöder SLO loggar du ut från ett program och loggar bara ut användaren för just det programmet. |
| Cachelagring | Programmerare | REST API-implementeringarna måste implementera sin egen cachningsmekanism för dataobjekt som överenskommits med företag. SDK:erna cachelagrar automatiskt olika dataobjekt, samtidigt som olika affärsregler beaktas. Användarens metadata cachelagras till exempel med samma TTL-värde som autentiseringstoken, medan vissa objekt programmässigt kan uteslutas från cachelagring (preflight). |
| Detaljerad felrapporteringsmekanism | Programmerare | REST API är i första hand beroende av HTTP-felkoder för att rapportera programfel, medan SDK:er har en detaljerad felrapporteringsmekanism som hjälper programutvecklarna att förstå vad som händer. |
| Återställning av programfel (försök igen vid fel, loopidentifiering osv.) | Programmerare | REST API-implementeringar måste bygga egna applikationsåterställningssystem medan implementeringar utöver SDK:er drar nytta av SDK:s felåterställningssystem: återställning från tillfälliga nätverksfel genom att försöka utföra vissa nätverksanrop med befintlig logik för att förhindra &quot;loopar&quot;. |
| Autentisering per begärande | Programmerare | Vissa programmeringsdokument kräver autentisering för varje webbplats/app, antingen av affärsskäl eller på grund av tekniska problem. SDK:erna tillämpar automatiskt detta baserat på TVE Dashboard-konfigurationen. REST API-implementerare måste implementera detta själva för att inte bryta mot affärsavtal eller för att kunna slutföra auktoriseringen för de MVPD-program som omfattar sina autentiseringsdata per program. |
| Passiv autentisering | Programmerare | Vissa MVPD-program stöder &quot;passiv&quot; autentisering, där användaren inte behöver ange inloggningsuppgifterna och ett försök att autentisera användaren görs automatiskt. Detta är särskilt användbart för distributörer av videofilmsprogram som även har&quot;Autentisering per begärande&quot; som ett krav. I så fall är användargränssnittet som aktiveras av SDK:er sömlöst, där användaren bara autentiserar en gång i ett program och SDK utför&quot;passiv&quot; autentisering för andra program i ekosystemet. Användaren ser inte de extra passiva samtalen, han eller hon kommer helt enkelt att vara autentiserad medan MVPD uppnår målet att ha separata autentiseringssessioner för varje program. |
| Implicit och enhetlig enhetsidentifiering | Programmerare | SDK:erna identifierar automatiskt enhetstypen och skickar informationen på ett standardsätt. REST API-implementeringar är benägna att skicka olika typer av information, beroende på implementeraren, vilket skevar/bryter mot affärsregler och statistik över olika webbplatser. **Programmerarna måste se till att de skickade oss korrekt enhetsinformation** i var och en av sina appar. För implementeringar från server till server identifierar REST api inte slutanvändarens IP-adress korrekt, såvida inte ytterligare åtgärder vidtas. IP-adressen är viktig i vissa fall, t.ex. för att förhindra bedrägeri eller för värdbussadaptern. |
| Tamper-bevis TempPass | Programmerare | Tvingande TempPass baseras på ett stabilt enhets-ID. SDK:erna använder maskinvaruinformation/fingeravtryckstekniker för att identifiera enheten och den här mekanismen är inte offentlig och därmed säkrare och kollisionsfri. För REST API-implementeringar måste programmerarna implementera sina egna algoritmer för enhetsidentifiering/fingeravtryck. |
| Enhetsbindning | Programmerare | Token som genereras på en enhet med ett program över SDK är inte portabla, vilket gör det svårt för en illasinnad användare att dela sina tokens och ge åtkomst till andra användare. Detta baseras på samma enhets-ID-mekanism som &quot;manipuleringsskyddet för TempPass&quot;. För REST API stannar tokens i molnet, vilket innebär att två enheter med samma enhets-ID som gör samma anrop får samma svar/åtkomst. Programmerarna måste se till att de har en robust, säker och kollisionsfri mekanism för att generera/allokera enhets-ID:n. |
| Förutsägbara och certifierade funktioner | Programmerare | Den befintliga uppsättningen funktioner i varje SDK är konsekvent, förutsägbar och fullständigt certifierad och testad. Vissa affärskrav uppfylls via SDK:er, vilket gör det riskabelt för programmeraren att bryta mot kontrakt när REST API används. REST API kan vara mer flexibelt, men Adobe garanterar att SDK-implementeringarna verkställer affärsbeslut och inställningar från TVE Dashboard. När det gäller klientlösa implementerar varje programmerare en egen deluppsättning av affärsreglerna som sveper över applikationerna vid en viss tidpunkt. |


1. Som en del av vårt nya One API-initiativ planerar vi att åtgärda den här begränsningen och att kunna tillämpa regler per plattform baserat på enhetsidentifieringen.

2. Adobe fortsätter att arbeta med alla större plattformar för att implementera enkel inloggning för plattformen som kan användas med vårt REST API. Vårt One API-initiativ kommer att erbjuda SSO-stöd mellan appar som implementeras med systemspecifika SDK:er och appar som implementeras med REST API.

## Lägsta enhetskrav {#min_reqs}

För att kunna använda Primetimes REST API för autentisering måste enheterna uppfylla eller överskrida de lägsta tekniska kraven som anges i REST API-avsnittet i [Primetime authentication Platform / Device / Tools Requirements document](#general_clientless_reqs).


