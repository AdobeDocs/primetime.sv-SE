---
title: Rapport-API
description: API för Auditude-rapport
exl-id: 50eb4869-3765-4591-8c41-794b29d50044
source-git-commit: 628544e38616715e83e0274ba26cf93302ce0e61
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 1%

---

# Rapport-API {#report-api}

Användargränssnittet har hanterade roller för kunder och för aktiveringsteamet (Adobe). Kunderna har tillgång till portalen och kan sedan skapa och redigera sina konfigurationer. De kan också se rapporterna om sina annonser i användargränssnittet.

API:er fungerar bakom kulisserna för att underlätta för kunder och administratörer att kommunicera med serverdelsinfrastrukturen.

För att utforska [!DNL Primetime Ad Insertion] API:er finns [Ad Insertion API-slutpunkter i växlat användargränssnitt](https://adconfigservice-va6.cloud.adobe.io/swagger-ui/index.html#/).

## API-slutpunkt {#report-api-endpoint}

### Produktion {#production}

`https://dai-primetime.adobe.io/report`

### Sandbox {#sandbox}

`https://dai-sandbox1-primetime.adobe.io/report`

## Frågeparametrar


| Namn | Signifikans | Värdetyp | Obligatoriskt? | Standardvärde | Begränsningar | Exempel/giltiga exempelvärden |
|----------|-----------------------------------------------------------------------------------------------|----------------|----------------|---------------------|------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| endDate | Slutdatum för rapportdata | datum | Y | INGEN | inte nyare än igår i UTC-8 | ######### |
| filter | filtrera en eller flera kolumner | string | N | INGEN | ad_config_id, zone_id | ad_config_id=990,900;state=active |
|  |  |  |  |  | När metaData är inställt på &#39;true&#39; i begäran kan du även filtrera efter namn. |  |
|  |  |  |  |  |  | Flera filternycklar är semikolonavgränsade. |
|  |  |  |  |  |  | Använd kommaavgränsade värden för att visa en lista med värden för filternyckeln |
| groupBy | Gruppera efter i tid ( år \| månad \| dag) eller ad_config_id. Adconfig är synonymt med AdRule. | string | N | INGEN | y \| m \| d , ad_config_id | m, ad_config_id |
|  |  |  |  |  |  |  |
|  |  |  |  |  |  | För groupBy i tid anger du antingen y eller m eller d |
|  |  |  |  |  |  |  |



## Sidhuvuden {#headers}

| Namn | Värdetyp | Obligatoriskt | Exempelvärde | Signifikans |
|-----------------------|----------------|---------------|-------------------------------------|------------------------------------|
| Acceptera | string | Y | text/csv för CSV | Typ av svar som förväntas från API |
|  |  |  | application/json or &#39;*/*&#39; för JSON |  |
| Auktoriseringstoken | string | Y | xyz | auktoriseringstoken |
| x-api-key | string | Y | xyz | API-nyckel |
| x-gw-ims-org-id | string | Y | xyz12345 | IMS-organisations-ID för ditt konto |

* Du kan generera en autentiseringstoken (kallas även åtkomsttoken) genom att följa stegen som beskrivs på hjälpsidan för JWT-autentisering i Adobe.io.
   >[!NOTE]
   >Auktoriseringstoken har ett förfallodatum på 24 timmar, så om du använder rapport-API med ett återkommande skript måste du generera en auth-token innan det går ut eller när du får ett Oauth-fel om att token inte är giltig.

* Om du vill ange rätt värden i begärandehuvudet och generera en autentiseringstoken (med JWT-autentisering) måste du känna till nedanstående konfigurationer för ditt konto. Kontakta supportteamet på Primetime för att få dessa värden.
ID för tekniskt konto

   * Org-id
   * API_tangent
   * Klient_hemlighet

## Utdata {#output}

Resultatet av en rapport-API-fråga är som standard i JSON-format, som anger avbildningar mot de olika värdena för de begärda dimensionerna (gruppera efter param). Nedan visas exempel på utdata:

```JSON
[
    {
        "dates": "07-2020",
        "total_impressions": 213007041
    },
    {
        "dates": "08-2020",
        "total_impressions": 174711626
    },
    {
        "dates": "09-2020",
        "total_impressions": 102863153
    }
]
```

## Felkoder och strängar {#error-codes-strings}

### Felsvarsformat {#error-response-format}

Fel vid återgivning av makrot &#39;code&#39;: Ett ogiltigt värde har angetts för parametern `com.atlassian.confluence.ext.code.render.InvalidValueException`

```Shell
{
"error_code": "<ERROR_CODE>",
"message": "<ERROR_MESSAGE>"
}
```

Tabellen nedan visar felkoder och meddelanden som kan returneras av rapport-API. Om du har problem med behörighetslagret kan du läsa [felkodsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#errors-and-troubleshooting) Adobe.io.

| Felkod | Felmeddelande |
|-----------------------|------------------------------------------|
| 4001007 | Användarinformationen är ogiltig. |
| 4001008 | Alla zoner kommer inte från samma konto. |
| 5001010 | Ett internt fel inträffade. |
| 4001011 | Datum skickas inte i det format som krävs. |
| 4001012 | Datumen ligger utanför intervallet. |
| 4001013 | Obligatorisk parameter saknas. |
| 4001014 | Zonlistan är tom för kontot. |
| 4001015 | Ogiltiga filternycklar i begäran. |
| 4001016 | Ogiltigt GroupBy-alternativ i begäran. |
| 4001017 | Ett ogiltigt ID har angetts i begäran |

## Exempelanrop och förväntade resultat {#sample-calls-expected-results}

Följande är kommandot curl för att få månatliga inställningsvärden mellan 2020-07-01 och 2021-06-30 med åtkomsttoken:

**Exempel på API-anrop**

```shell
curl --location --request GET 'https://dai-sandbox1-primetime.adobe.io/report?startDate=2020-07-01&endDate=2021-06-30&groupBy=m&unpaged=true' \
--header 'x-api-key: <API_KEY>' \
--header 'x-gw-ims-org-id: <ORG_ID>' \
--header 'Authorization: Bearer <ACCESS_TOKEN_STRING>' \
--header 'Accept: application/json'
```

| Exempel på samtal/användningsfall | Förväntat resultat |
|---|---|
| Hämta rapport med GET för start- och slutdatum: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2021-01-01: Acceptera = application/json. eller */* | Json med följande parametrar med alla annonser som tillhör det här kontot total_imponsions |
| Hämta rapport med GroupBy = d \| m \| y GET: [API_ENDPOINT]//report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d \| m \| y header : Acceptera = application/json. eller */* | JSON med följande parametrar och alla annonser som hör till dessa kontodatum (mm-dd-åååå \| mm-åååå \| yyyy format) total_impressions |
| Hämta rapport med GroupBy = ad_config_id-GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=ad_config_id header : Acceptera = application/json. eller */* | Json med följande parametrar med alla annonser som hör till det här kontot, ad_config_id total_imponsions |
| Hämta rapport med GroupBy = d \| m \| y och ad_config_id GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;groupBy=d,ad_config_id header : Acceptera = application/json. eller */* | JSON med följande parametrar och alla annonser som hör till det här kontot, ad_config_id-datum (mm-dd-åååå \| mm-åååå \| yyyy-format) total_imponsions |
| Hämta rapport med metaData=true och groupBy=d \| m \| med GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=ad_config_id header : Acceptera = application/json. eller */* | Json med följande parametrar med alla annonser som tillhör det här kontot ad_config_id name total_impressions |
| Hämta rapport med groupBy=d \| m \| y och ad_config_id-GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-05-01&amp;metaData=true&amp;groupBy=d \| m \| y,ad_config_id header : Acceptera = application/json. eller */* | JSON med följande parametrar och alla annonser som hör till det här kontot, ad_config_id name total_imponsions, datum (mm-dd-yyyy \| mm-yyyy \| yyy format) |
| Hämta rapport för att hämta alla rader för ett givet datumintervall (med unpaged = true) GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;groupBy=d&amp;unpaged=true | 31 poster i den returnerade Json-arrayen |
| Hämta rapport med giltig GET för sidfrågeparametrar: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-31&amp;page=0&amp;size=5&amp;groupBy=d | 5 poster i den returnerade arrayen |
| Hämta rapport, med GET i CSV-format: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10 header : Acceptera = text/csv | CSV-strängen returneras med rubriken: total_imponations |
| Hämta rapport, med CSV-format och groupBy = d \| m \| y GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;groupBy=d\|m\|y header : Acceptera = text/csv | CSV-strängen returneras med rubriken: total_imponsions, datum (mm-dd-åååå \| mm-åååå \| yyy format) |
| Hämta rapport, med csv-format, och metadata = true GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true header : Acceptera = text/csv | CSV-strängen returneras med rubriken: total_imponations |
| Hämta rapport, med csv-format, metadata = true och groupBy = d \| m \| via GET: [API_ENDPOINT]/report?startDate=2020-01-01&amp;endDate=2020-01-10&amp;metaData=true&amp;groupBy=d\|m\|y header : Acceptera = text/csv | CSV-strängen returneras med rubriken: total_imponsions, datum (mm-dd-åååå \| mm-åååå \| yyy format) |


## API-begränsningsprincip för rapport {#report-api-throttling-policy}

* 5 API-begäranden tillåts under 5 sekunders fönstertid för varje användare.
* Om en användare korsar över gränsen fördröjs svaret med 5 sekunder.
* Om en användare ringer mer än 10 samtal inom 5 sekunder börjar han/hon att bli avvisad med svaret&quot;429 Alltför många förfrågningar&quot;.
