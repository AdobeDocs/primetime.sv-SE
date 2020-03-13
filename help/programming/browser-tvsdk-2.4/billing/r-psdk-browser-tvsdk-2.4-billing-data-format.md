---
description: Webbläsarens TVSDK skickar faktureringsstatistik till Adobe i XML-format.
seo-description: Webbläsarens TVSDK skickar faktureringsstatistik till Adobe i XML-format.
seo-title: Skicka faktureringsmått
title: Skicka faktureringsmått
uuid: ed2638d2-7894-4840-b31a-51e48e0a3f49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Skicka faktureringsmått{#transmit-billing-metrics}

Webbläsarens TVSDK skickar faktureringsstatistik till Adobe i XML-format.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Om du använder ett verktyg för nätverksregistrering för att övervaka statistiken som Browser TVSDK överför till Adobe bör du se enheter som följande:

```
<?xml version="1.0" encoding="UTF-8"?>
<request>
    <sc_xml_ver>1.0</sc_xml_ver>
    <reportSuiteID>primesample2</reportSuiteID>
    <visitorID>947310128cb56f41</visitorID>
    <pageURL>https://. . ..m3u8</pageURL>
    <timestamp>2016-4-7T10:1:4</timestamp>
    <contextData>
        <billingMetrics>
            <publisherID>com.adobe.primetime.reference.PrimetimeReference</publisherID>
            <contentType>vod</contentType>
            <adsEnabled>true</adsEnabled>
            <midrollEnabled>true</midrollEnabled>
            <platform>Mac OSX 10.11.5</platform>
            <tvsdkVersion>2,4,0,1559</tvsdkVersion>
            <contentURL>https://. . ..m3u8</contentURL>
        </billingMetrics>
    </contextData>
</request>
```

De booleska egenskaperna `drmProtected`, `adsEnabled`och `midrollEnabled` visas bara om de är sanna.