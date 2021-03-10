---
description: Webbläsarens TVSDK skickar faktureringsvärden till Adobe i ett XML-format.
title: Skicka faktureringsmått
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---


# Skicka faktureringsmått{#transmit-billing-metrics}

Webbläsarens TVSDK skickar faktureringsvärden till Adobe i ett XML-format.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Om du använder ett verktyg för nätverksinspelning för att övervaka statistik Browser TVSDK-överföringar till Adobe bör du se enheter som följande:

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

De booleska egenskaperna `drmProtected`, `adsEnabled` och `midrollEnabled` visas bara om de är sanna.