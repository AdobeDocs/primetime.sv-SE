---
title: Översikt över försämringsAPI
description: Översikt över försämringsAPI
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Översikt över försämringsAPI {#degradation-api-overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Allmän information {#general_info}

>[!NOTE]
>
>Detta API är inte allmänt tillgängligt. Kontakta din Adobe-representant för att få uppdateringar.

Den här funktionen ger alla tre parter i en integrering (programmerare, distributörer av videoprogrammeringstjänster och Adobe) möjlighet att tillfälligt kringgå specifika slutpunkter för MVPD-autentisering och -auktorisering. Vanligtvis är det Programmeraren som initierar en sådan åtgärd, men oavsett vem som utlöser en nedbrytningshändelse beror åtgärden på hur man tidigare kommit överens om arrangemang med de berörda PDF-filerna.

Det viktigaste användningsexemplet för den här funktionen är live-sporter eller stora event. I sådana höga trafikscenarier är det möjligt att belastningen på en specifik MVPD-slutpunkt blir för hög, vilket ger mycket långa svarstider för användarna. För att bevara en bra användarupplevelse under ett sådant scenario kan programmeraren besluta att utlösa en försämringsregel som tillfälligt kan autenticera/autoauktorisera användare, eller inaktivera ett MVPD genom att ta bort det från listan över tillgängliga MVPD.

En försämringsregel tillämpas bara under en fast tidsperiod. Även om de primära kunderna för den här funktionen är sportkanaler och dynamiska nyhetskanaler, kan alla programmerare vilja ha tillgång till den här funktionen, eftersom programmerartjänsterna då och då är desamma.

Försämringskommentarer:

* Den här funktionen är avsedd att användas tillsammans med API:t för användningsövervakning, som ger realtidsinformation om antalet autentiseringar och auktoriseringar per MVPD, genomsnittlig auktoriseringsfördröjning och andra mått som behövs för en fullständig serviceöversikt.
* Den här funktionen tillåter inte att autentiseringstjänsten Adobe Primetime kringgås. Om Primetime-autentisering saknas finns det ingen mekanism i tjänsten som kan användas för att tillåta användare att se innehåll. Webbplatserna eller apparna kan dock själva dirigera runt Primetime-autentisering.
* Adobe kommer för närvarande inte att utlösa någon direkt försämring - beslutet måste alltid fattas med en särskild programmerare som har godkänt sådana villkor med sidoskyddsprogram. I framtiden kan Primetime-autentisering vara proaktiv när det gäller att utlösa försämringsregler om avtal (SLA-skydd) kan nås med sidoskyddsprogram.

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->