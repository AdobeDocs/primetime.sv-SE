---
title: Tillståndsövervakningens översikt
description: Tillståndsövervakningens översikt
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---


# Tillståndsövervakningens översikt {#entitlement-service-monitoring-overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion {#introduction}

TVE-sajter och -appar måste vara tillgängliga dygnet runt, så kunderna behöver realtidsinsikter i berättigandehändelser för att kunna upptäcka och korrigera problem så snabbt som möjligt. De måste också analysera månadsdata för att avgöra vilka plattformar som tillhandahåller större delen av trafiken, och vilka plattformar som kan ha dålig implementering och dålig konverteringsgrad.

ESM (Entitlement Service Monitoring) ger programmerare och distributörer av videoprogrammeringstjänster en datafeed som ger realtidsinsyn i deras autentiserings- och auktoriseringshändelser. Data samlas in från Adobe Primetime autentiseringssystem och tillhandahålls via ett RESTful API.  Kunderna kan förbruka data direkt eller från sina egna skräddarsydda kontrollpaneler.

ESM-systemets kärnelement är dess mått och mått. ESM genererar rapporter som innehåller aggregerade mätvärden enligt dimensionsurvalet. När Adobe Pass-händelser är inloggade i PST-tidszonen är ESM-rapporterna också tillgängliga i PST-tidszonen. 

ESM API är inte allmänt tillgängligt.  Kontakta din Adobe-representant om du har frågor om tillgänglighet.

## ESM för programmerare {#esm-for-programmers}

### Programmerare kan övervaka följande mätvärden: {#programmers-monitor-metrics}


| *Måttnamn* | *Beskrivning* |
|-------------------------|--------------------------|
| autentiseringsförsök | Antal initierade autentiseringsflöden |
| lyckad | Antal autentiseringstoken som har hämtats av klienter |
| författarväntande | Antal autentiseringstoken som genererats (oavsett om klienten verkligen fått den eller inte) |
| authn-failed | Antal misslyckade autentiseringar som utförts via ett externt system. |
| clientless-tokens | Antal klientlösa token som har skickats |
| klientlösa fel | Antal misslyckade försök att ta emot tokens från klientlöst API |
| authz-try | Antal försök till auktorisering |
| authz-success | Antal godkända auktoriseringar |
| authz-failed | Antal nekade auktoriseringar av sidoskyddsprogram på programnivå |
| authz-jected | Antal försök till auktorisering som anses vara skadliga av Adobe Service Provider och som avvisats som ett resultat av DoS-attacker |
| authz-latency | Totalt antal millisekunder som har ägnats åt MVPD-slutpunkten |
| media-tokens | Antal genererade korta medietoken (som motsvarar antalet uppspelningsbegäranden) |
| unika konton | Antal unika användare som har utfört berättigandeåtgärder (AuthN/AuthZ) i det valda tidsintervallet. (Det här måttet visas bara om dygnsvärden begärs.) </br> Detta beräknas för varje enskilt datacenter. När dc-dimensionen inte har begärts visas inte det här måttet. |
| unika sessioner | Antal unika sessioner som har utfört autentiseringsflödesanrop till Adobe Primetime-autentiseringstjänsten inom det valda tidsintervallet. (Det här måttet visas bara om dygnsvärden begärs.) </br> Detta beräknas för varje enskilt datacenter. När dc-dimensionen inte har begärts visas inte det här måttet. |
| antal | En enkel räknare som används i händelseorienterade rapporter |

</br>

### Programmerare kan filtrera mätvärdena som listas ovan efter följande mått: {#progr-filter-metrics}


| *Dimensionens namn* | *Beskrivning* |
|---|---|
| år | Det fyrsiffriga året |
| månad | Månad på året (1-12) |
| dag | Dag i månaden (1-31) |
| timme | Timme på dagen |
| minut | Minut av timmen |
| medieföretag | Medieföretaget som äger webbplatsen som initierade berättigandeprocessen för användaren |
| dc | (Datacenter) Hemregionen där begäran togs emot. |
| proxy | Proxyvariabeln MVPD (som kommer att vara &quot;Direkt&quot; för direkta integreringar) |
| mvpd | Det huvuddokument som ansvarar för att bevilja behörighet till användaren |
| beställar-id | ID för begärande som används för att utföra berättigandebegäran |
| kanal | Kanalwebbplatsen, som har extraherats från resursfältet (extraherats från MRSS-nyttolasten som kanal/titel om sådan finns, eller mappats till resursvärdet om det inte är i RSS-format). |
| resource-id | Den faktiska resurstitel som ingår i auktoriseringsbegäran (extraherad från MRSS-nyttolasten som artikel/titel om sådan finns) |
| enhet | Enhetsplattformen (dator, mobil, konsol osv.) |
| ap | Den externa autentiseringsprovidern när autentiseringsflödet utförs via ett externt system. </br> Värdena kan vara: </br> - Ej tillämpligt - autentiseringen tillhandahölls av Primetime-autentisering </br> - Apple - det externa system som tillhandahöll autentiseringen är Apple |
| os-family | Operativsystem som körs på enheten |
| webbläsarfamiljen | Användaragent som används för åtkomst till Adobe Primetime-autentisering |
| cdt | Enhetsplattformen (alternativ) som för närvarande används för klientlösa. </br>  Värdena kan vara: </br> - Ej tillämpligt - händelsen kom inte från en klientlös SDK </br> - Okänd - Eftersom parametern deviceType från ett klientlöst API är valfri finns det anrop som inte innehåller något värde. </br> - alla andra värden som skickades via det klientlösa API:t, t.ex. xbox, appletv, roku osv. </br> |
| platform-version | Versionen av SDK utan klient |
| os-type | Operativsystem som körs på enheten, alternativ (används inte för närvarande) |
| webbläsarversion | Användaragentversion |
| sdk-typ | Klient-SDK som används (Flash, HTML5, Android-modernt, iOS, klientlöst osv.) |
| sdk-version | Versionen av Adobe Primetime autentiseringsklient-SDK |
| event | Adobe Primetime-autentiseringshändelsens namn |
| orsak | Orsaken till fel, enligt Adobe Primetime-autentisering |
| sso-type | Den underliggande SSO-mekanismen: platform/passive/adobe. Anger att auktoriseringstoken utfärdades genom att AuthN återanvändes i ett annat program |

## ESM för MVPD {#esm-for-mvpds}

### MVPD-program kan övervaka följande mått:

| *Måttnamn* | *Beskrivning* |
|---|---|
| autentiseringsförsök | Antal initierade autentiseringsflöden |
| lyckad | Antal autentiseringstoken som har hämtats av klienter |
| författarväntande | Antal autentiseringstoken som genererats (oavsett om klienten verkligen fått den eller inte) |
| authn-failed | Antal misslyckade autentiseringar som utförts via ett externt system. |
| authz-try | Antal försök till auktorisering |
| authz-success | Antal godkända auktoriseringar |
| authz-failed | Antal nekade auktoriseringar av sidoskyddsprogram på programnivå |
| authz-jected | Antal försök till auktorisering som anses vara skadliga av Adobe Service Provider och som avvisats som ett resultat av DoS-attacker |
| authz-latency | Totalt antal millisekunder som har ägnats åt MVPD-slutpunkten |

### MVPD-program kan filtrera mätvärdena som anges ovan med följande mått:

| *Dimensionens namn* | *Beskrivning* |
|---|---|
| år | Det fyrsiffriga året |
| månad | Månad på året (1-12) |
| dag | Dag i månaden (1-31) |
| timme | Timme på dagen |
| minut | Minut av timmen |
| beställar-id | ID för begärande som används för att utföra berättigandebegäran |
| ap | Den externa autentiseringsprovidern när autentiseringsflödet utförs via ett externt system. </br> Värdena kan vara: </br> - Ej tillämpligt - autentiseringen tillhandahölls av Primetime-autentisering </br> - Apple - det externa system som tillhandahöll autentiseringen är Apple |
| cdt | Enhetsplattformen (alternativ) som för närvarande används för klientlösa. </br>  Värdena kan vara: </br> - Ej tillämpligt - händelsen kom inte från en klientlös SDK </br> - Okänd - Eftersom parametern deviceType från ett klientlöst API är valfri finns det anrop som inte innehåller något värde. </br> - alla andra värden som skickades via det klientlösa API:t, t.ex. xbox, appletv, roku osv. </br> |
| sdk-typ | Klient-SDK som används (Flash, HTML5, Android-modernt, iOS, klientlöst osv.) |


## Användningsexempel {#use-cases}

Du kan använda ESM-data för följande användningsområden:

- **Övervakning** - Ops- och övervakningsteam kan skapa en kontrollpanel eller diagram som anropar API:n varje minut. Med hjälp av den information som visas kan de upptäcka ett problem (med Primetime-autentisering eller med ett MVPD) så fort det visas.  

- **Felsökning/kvalitetstestning** - Eftersom data också delas upp efter plattform, enhet, webbläsare och operativsystem kan analysmönster identifiera problem med specifika kombinationer (t.ex. Safari på OSX).  

- **Analyser** - De data som tillhandahålls kan användas för att komplettera/granska data på klientsidan som samlas in via Adobe Analytics eller något annat analysverktyg.

<!--
## Related Information {#related-information}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->