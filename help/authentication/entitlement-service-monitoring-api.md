---
title: API för tillståndsövervaknings-API
description: API för tillståndsövervaknings-API
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2026'
ht-degree: 0%

---


# API för tillståndsövervaknings-API {#entitlement-service-monitoring-api}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## API-översikt {#api-overview}

ESM (Entitlement Service Monitoring) implementeras som en WOLAP (webbaserad [Analytisk onlinebearbetning](https://en.wikipedia.org/wiki/Online_analytical_processing){target=_blank}). ESM är ett generiskt webb-API för företagsrapportering som backas upp av data warehouse. Det fungerar som ett HTTP-frågespråk som gör att vanliga OLAP-åtgärder kan utföras RESTfully.

>[!NOTE]
>
>ESM API är inte allmänt tillgängligt. Kontakta din Adobe-representant om du har frågor om tillgänglighet.

ESM-API:t ger en hierarkisk vy över de underliggande OLAP-kubarna. Varje resurs ([dimension](#esm_dimensions) i dimensionshierarkin, mappad som ett URL-sökvägssegment) genererar rapporter med (aggregerad) [mått](#esm_metrics) för den aktuella markeringen. Varje resurs pekar på sin överordnade resurs (för sammanslagning) och dess underresurser (för fördjupning). Segmentering och segmentering uppnås med frågesträngsparametrar som fäster dimensioner till specifika värden eller intervall.

REST API tillhandahåller tillgängliga data inom ett tidsintervall som anges i begäran (som faller tillbaka till standardvärdena om inget anges), enligt dimensionssökvägen, tillhandahållna filter och valda mätvärden. Tidsintervallet används inte för rapporter som inte innehåller tidsdimensioner (år, månad, dag, timme, minut, sekund).

Slutpunkts-URL-rotsökvägen returnerar sammanställda mått inom en enda post, tillsammans med länkarna till de tillgängliga detaljalternativen. API-versionen mappas som det avslutande segmentet i URI-sökvägen för slutpunkten. Till exempel: `https://mgmt.auth.adobe.com/*v2*` innebär att klienterna kommer åt WOLAP version 2.

De tillgängliga URL-sökvägarna kan identifieras via länkar i svaret. Giltiga URL-sökvägar hålls för att mappa en sökväg i det underliggande fördjupningsträdet som innehåller (pre-) aggregerade mått. En bana i formuläret `/dimension1/dimension2/dimension3` återspeglar en föraggning av dessa tre dimensioner (motsvarigheten till en SQL `clause GROUP` AV `dimension1`, `dimension2`, `dimension3`). Om det inte finns någon sådan föraggning och systemet inte kan beräkna den direkt, returnerar API:t ett 404-svar som inte hittades.

## Detaljträd {#drill-down-tree}

Följande nedåtriktade träd visar dimensionerna (resurserna) som finns i ESM 2.0 för [Programmerare] (#esm_dimensions) och [MVPD](#esm_dimensions_mvpd).


### Dimensioner för programmerare {#progr-dimensions}

![](assets/esm-progr-dimensions.png)

### Dimensioner tillgängliga för distributörer av videoprogrammeringstjänster {#mvpd-dimensions}

![](assets/esm-mvpd-dimensions.png)

En GET till `https://mgmt.auth.adobe.com/v2` API-slutpunkten returnerar en representation som innehåller:

* Länkar till tillgängliga rotsökvägar:

   * `<link rel="drill-down" href="/v2/dimensionA"/>`

   * `<link rel="drill-down" href="/v2/dimensionB"/>`

* En sammanfattning (aggregerade värden) för alla mått (i standardintervallet, eftersom inga frågesträngsparametrar anges, se nedan).


Så här visar du en detaljerad sökväg (steg för steg):
`/dimensionA/year/month/day/dimensionX` hämtar följande svar:

* Länkar till`dimensionY`&quot; och &quot;`dimensionZ`&quot; detaljeringsalternativ

* En rapport som innehåller dagliga aggregat för varje värde av `dimensionX`


### Filter

Förutom datum-/tidsdimensionerna kan alla dimensioner som är tillgängliga för den aktuella projektionen (dimensionssökväg) filtreras genom att använda dess namn som en frågesträngsparameter.

Följande filtreringsalternativ är tillgängliga:

* **Lika med** filter anges genom att dimensionsnamnet ställs in på ett visst värde i frågesträngen.

* **IN** Du kan ange filter genom att lägga till samma dimension-name-parameter flera gånger med olika värden: dimension=värde1\&amp;dimension=värde2

* **Inte lika med** filter måste använda &#39;\!&#39; symbolen efter dimensionsnamnet som resulterar i tecknet &#39;\!=&#39; &quot;operator&quot;: dimension\!=värde

* **INTE IN** -filter kräver \!=&#39; operatorn ska användas flera gånger, en gång för varje värde i uppsättningen: dimension\!=värde1\&amp;dimension\!=värde2&amp;...

Det finns också en särskild användning för dimensionsnamnen i frågesträngen: Om dimensionsnamnet används som en frågesträngsparameter utan värde instrueras API:t att returnera en projektion som innehåller den dimensionen i rapporten.

### Exempel på ESM-frågor

| *URL* | *SQL-motsvarighet* |
|---|---|
| /dimension1/dimension2/dimension3?dimension1=värde1 | SELECT * from projection WHERE dimension1 = &#39;value1&#39; </br> GROUP BY dimension1, dimension2, dimension3 |
| /dimension1/dimension2/dimension3?dimension1=värde1&amp;dimension1=värde2 | SELECT * from projection WHERE dimension1 IN (&#39;value1&#39;, &#39;value2&#39;) </br> GROUP BY dimension1, dimension2, dimension3 |
| /dimension1/dimension2/dimension3?dimension1!=value1 | SELECT * from projection WHERE dimension1 &lt;> &#39;value1&#39; | </br> GROUP BY dimension1, dimension2, dimension3 |
| /dimension1/dimension2/dimension3?dimension1!=värde1&amp;dimension2!=value2 | SELECT * from projection WHERE dimension1 NOT IN (&#39;value1&#39;, &#39;value2&#39;) | </br> GROUP BY dimension1, dimension2, dimension3 |
| Anta att det inte finns någon direkt sökväg: /dimension1/dimension3 </br> men det finns en sökväg: /dimension1/dimension2/dimension3 </br> </br> /dimension1?dimension3 | SELECT * from projection GROUP BY dimension1, dimension3 |

>[!NOTE]
>
>Ingen av dessa filtertekniker fungerar för `date/time` dimensioner. Det enda sättet att filtrera `date/time` dimensionerna är för att ange `start` och `end` frågesträngsparametrar (beskrivs nedan) till de värden som krävs.

Följande frågesträngsparametrar har reserverade betydelser för API (och kan därför inte användas som dimensionsnamn, annars går det inte att filtrera en sådan dimension).

### ESM API Reserved Query String Parameters

| Parameter | Valfritt | Beskrivning | Standardvärde | Exempel |
| --- | ---- | --- | ---- | --- |
| access_token | Ja | Om IMS OAuth-skyddet är aktiverat kan IMS-token skickas antingen som en standardtoken för auktorisering Bearer eller som en frågesträngsparameter. | Ingen | access_token=XXXXXX |
| dimension-namn | Ja | Dimensionsnamn - antingen i den aktuella URL-sökvägen eller i en giltig delsökväg. värdet behandlas som ett lika med-filter. Om inget värde anges kommer den angivna dimensionen att inkluderas i utdata även om den inte finns med eller intill den aktuella banan | Ingen | someDimension=someValue&amp;someOtherDimension |
| end | Ja | Sluttid för rapporten i millisekunder | Serverns aktuella tid | end=2012-07-30 |
| format | Ja | Används för innehållsförhandling (med samma effekt men lägre prioritet än sökvägen &quot;extension&quot; - se nedan). | Ingen: kommer innehållsförhandlingen att försöka med andra strategier | format=json |
| limit | Ja | Maximalt antal rader som ska returneras | Standardvärde som rapporteras av servern i självlänken om ingen gräns anges i begäran | limit=1500 |
| mått | Ja | Kommaavgränsad lista med metriska namn som ska returneras. Detta bör användas både för att filtrera en delmängd av de tillgängliga mätvärdena (för att minska nyttolaststorleken) och för att tvinga API att returnera en projektion som innehåller de begärda mätvärdena (i stället för den optimala standardprojektionen). | Alla mätvärden som är tillgängliga för den aktuella projektionen returneras om den här parametern inte anges. | metrics=m1,m2 |
| start | Ja | Starttid för rapporten som ISO8601. servern fyller i den återstående delen om bara ett prefix anges: Exempel: start=2012 kommer att resultera i start=2012-01-01:00:00:00 | rapporteras av servern i självlänken, servern försöker tillhandahålla rimliga standardvärden baserat på den valda tidsperioden | start=2012-07-15 |

Den enda tillgängliga HTTP-metoden är GET. Stöd för OPTIONS/HEAD kan ges i framtida versioner.

## ESM API-statuskoder {#esm-api-status-codes}

| Statuskod | Orsaksfras | Beskrivning |
|---|---|---|
| 200 | OK | Svaret kommer att innehålla länkarna &quot;roll-up&quot; och &quot;drill-down&quot; (om tillämpligt). Rapporten återges som ett attribut för resursen: ett kapslat rapportelement/en kapslad rapportegenskap. |
| 400 | Felaktig begäran | Svarstexten innehåller ett textmeddelande som förklarar vad som är fel med begäran. </br> </br> Statusen 400 Dålig begäran åtföljs av en förklarande text i svarstexten (normal/textmedietyp) som ger användbar information om klientfelet. Förutom de triviala scenarierna, till exempel ogiltiga datumformat eller filter som tillämpas på icke-befintliga dimensioner, kommer systemet också att neka att svara på frågor som kräver att en stor mängd data returneras eller slås samman i farten. |
| 401 | Obehörig | Orsakas av en begäran som inte innehåller rätt OAuth-huvuden för att autentisera användaren |
| 403 | Förbjuden | Anger att begäran inte tillåts i den aktuella säkerhetskontexten. detta inträffar när användaren är autentiserad men inte har behörighet att komma åt den begärda informationen |
| 404 | Hittades inte | Inträffar om en ogiltig URL-sökväg anges med begäran. Detta bör aldrig inträffa om klienten följer länkarna &quot;drill-down&quot;/&quot;roll-up&quot; som finns i 200 svar |
| 405 | Metoden tillåts inte | Signalerar att en metod som inte stöds användes i begäran. Även om det för närvarande bara finns stöd för metoden GET kan framtida versioner tillåta HEAD eller OPTIONS |
| 406 | Godkänns inte | Signalerar att en medietyp som inte stöds begärdes av klienten |
| 500 | Internt serverfel | &quot;Det här ska aldrig hända&quot; |
| 503 | Tjänsten är inte tillgänglig | Signalerar ett fel i programmet eller dess beroenden |

## Dataformat {#data-formats}

Data finns i följande format:

* JSON (standard)
* XML
* CSV
* HTML (för demoändamål)

Följande strategier för innehållsförhandling kan användas av klienter (prioriteten ges av positionen i listan - första saker först):

1. Ett filtillägg som läggs till i det sista segmentet i URL-sökvägen: t.ex. `/esm/v2/media-company/year/month/day.xml`. Om URL:en innehåller en frågesträng måste tillägget komma före frågetecknet: `/esm/v2/media-company/year/month/day.csv?mvpd= SomeMVPD`
1. En formatfrågesträngsparameter: t.ex. `/esm/report?format=json`
1. Standardrubriken för HTTP-godkännande: t.ex. `Accept: application/xml`

Både &quot;extension&quot; och frågeparametern stöder följande värden:

* xml
* json
* csv
* html

Om ingen medietyp har angetts i någon av strategierna skapar API-gränssnittet JSON-innehåll som standard.

## Hypertext Application Language {#hypertext-application-language}

För JSON och XML kommer nyttolasten att kodas som HAL, vilket beskrivs här:  <http://stateless.co/hal_specification.html>.

Den faktiska rapporten (en kapslad tagg/egenskap som kallas&quot;rapport&quot;) består av den faktiska listan med poster som innehåller alla valda/tillämpliga mått och mått med deras värden, kodade enligt följande:

### JSON

```JSON
 "report": [
  {
    "dimension1": "d1",
    ...
    "metric1": "m1",
    ...
  }, {
    ...
  }
]
```

### XML

```XML
 <report>
  <record dimension1="d1" ... metric1="m1" ... />
  ...
</report
```

För XML- och JSON-format är fältordningen (mått och mått) i en post ospecificerad - men konsekvent (ordningen är densamma i alla poster). Klienter bör dock inte förlita sig på någon särskild ordning för fälten i en post.

Resurslänken (self-rel i JSON och href-resursattributet i XML) innehåller den aktuella sökvägen och frågesträngen som används för den infogade rapporten. Frågesträngen visar alla implicita och explicita parametrar så att nyttolasten uttryckligen anger vilket tidsintervall som används, eventuella implicita filter och så vidare. Resten av länkarna i resursen innehåller alla tillgängliga segment som kan följas för att detaljgranska aktuella data. En länk för sammanslagning kommer också att anges och den kommer att peka på den överordnade sökvägen (om sådan finns). The `href` värdet för länkarna för detaljnivå/rollup innehåller bara URL-sökvägen (den innehåller inte frågesträngen, så klienten måste lägga till den om det behövs). Observera att inte alla frågesträngsparametrar som används (eller är underförstådda) av den aktuella resursen kan användas för länkar av typen &quot;roll-up&quot; eller &quot;drill-down&quot; (filtren kan till exempel inte gälla för underresurser eller superresurser).

Exempel (förutsatt att vi har ett enda mått som kallas `clients` och det finns en föraggning för `year/month/day/...`):

* https://mgmt.auth.adobe.com/esm/v2/year/month.xml

```XML
   <resource href="/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21">
   <links>
   <link rel="roll-up" href="/esm/v2/year"/>
   <link rel="drill-down" href="/esm/v2/year/month/day"/>
   </links>
   <report>
   <record month="6" year="2012" clients="205"/>
   <record month="7" year="2012" clients="466"/>
   </report>
   </resource>
```

* https://mgmt.auth.adobe.com/esm/v2/year/month.json 

   ```JSON
       {
         "_links" : {
           "self" : {
             "href" : "/esm/v2/year/month?start=2012-07-20T00:00:00&end=2012-08-20T14:35:21"
           },
           "roll-up" : {
             "href" : "/esm/v2/year"
           },
           "drill-down" : {
             "href" : "/esm/v2/year/month/day"
           }
         },
         "report" : [ {
           "month" : "6",
           "year" : "2012",
           "clients" : "205"
         }, {
           "month" : "7",
           "year" : "2012",
           "clients" : "466"
         } ]
       }
   ```

### CSV

I CSV-dataformatet kommer inga länkar eller andra metadata (med undantag för rubrikraden) att anges. i stället anges urvalsmetadata i filnamnet, som kommer att följa detta mönster:

```CSV
    esm__<start-date>_<end-date>_<filter-values,...>.csv
```

CSV-filen innehåller en rubrikrad och sedan rapportdata som efterföljande rader. Rubrikraden innehåller alla mått följt av alla mått. Sorteringsordningen för rapportdata återspeglas i dimensionernas ordning. Om data därför sorteras efter `D1` och sedan `D2`ser CSV-rubriken ut så här: `D1, D2, ...metrics...`.

Fältens ordning i rubrikraden återspeglar sorteringsordningen för tabelldata.


Exempel: https://mgmt.auth.adobe.com/v2/year/month.csv skapar en fil med namnet `report__2012-07-20_2012-08-20_1000.csv` med följande innehåll:


| År | Månad | Klienter |
| ---- | :---: | ------- |
| 2012 | 6 | 580 |
| 2012 | 7 | 231 |

## Datahastighet {#data-freshness}

De lyckade HTTP-svaren innehåller en `Last-Modified` rubrik som anger tidpunkten då rapporten i brödtexten senast uppdaterades. Avsaknaden av en senast ändrad rubrik anger att rapportdata beräknas i realtid.

Oftast uppdateras grova grå data mindre ofta än finkorniga data (t.ex. minutvärden eller timvärden kan vara mer aktuella än de dagliga värdena, särskilt för mätvärden som inte kan beräknas utifrån mindre granularitet, t.ex. unika tal).

Framtida versioner av ESM kan göra det möjligt för klienter att utföra villkorliga GET-filer genom att ange standardrubriken&quot;If-Modified-Since&quot;.

## GZIP-komprimering {#gzip-compression}

Adobe rekommenderar starkt att du aktiverar GZIP-stöd i klienter som hämtar ESM-rapporter. Om du gör det minskar svarsstorleken avsevärt, vilket i sin tur minskar svarstiden. (Komprimeringsförhållandet för ESM-data ligger i intervallet 20-30.)

Om du vill aktivera gzip-komprimering i klienten anger du `Accept-Encoding:` sidhuvud enligt följande:

* Accept-Encoding: gzip, tömma


<!--
## Related Information {#related-information}

- [ESM Overview](/help/authentication/entitlement-service-monitoring-overview.md)
- [Degradation API Overview](/help/authentication/degradation-api-overview.md)
- [Understanding Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->