---
description: För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.
title: Faktureringsanvändningsstatistik
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# Faktureringsmått {#billing-metrics}

För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.

Varje gång spelaren genererar en direktuppspelningshändelse börjar TVSDK skicka HTTP-meddelanden regelbundet till Adobe faktureringssystem. Perioden, som kallas fakturerbar varaktighet, kan vara en annan för VOD av standardtyp, VOD av proffskvalitet (aktiverad annonsering i mellanrullar) och direktinnehåll. Standardlängden för varje innehållstyp är 30 minuter, men ditt kontrakt med Adobe avgör de faktiska värdena.

Meddelandena innehåller följande information:

* Innehållstyp (live, linear eller VOD)
* Innehålls-URL
* Om annonser är aktiverade
* Anger om annonser på mellannivå är aktiverade (endast VOD)
* Anger om strömmen skyddas av DRM
* Version och plattform för TVSDK

Adobe förkonfigurerar det här arrangemanget, men om du vill ändra ordningen ska du arbeta med din representant för Adobe Enablement.

Om du vill övervaka den statistik som TVSDK skickar till Adobe hämtar du URL-adressen från Adobe Enablement-representanten och använder ett verktyg för nätverksregistrering, till exempel Charles, för att se data.

## Konfigurera faktureringsmått {#configure-billing-metrics}

Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du har fått andra konfigurationsparametrar från din Adobe-representant kan du använda klassen PTBillingMetricsConfiguration för att ställa in de här parametrarna innan du initierar mediespelaren.

De flesta kunder bör använda standardkonfigurationen.

>[!IMPORTANT]
>
>Den konfiguration du anger gäller så länge mediespelaren är aktiv. När du har initierat mediespelaren kan du inte ändra konfigurationen.

Så här konfigurerar du faktureringsmått:

Ange följande kodexempel.

```
PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
billingConfig.enabled = YES; 
billingConfig.stdVODBillableDurationMinutes = 60.0; 
billingConfig.proVODBillableDurationMinutes = 30.0; 
billingConfig.liveBillableDurationMinutes = 15.0; 
                
// metadata is the PTMetadata instance set on PTMediaPlayerItem 
[metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
```

## Skicka faktureringsmått {#transmit-billing-metrics}

TVSDK skickar faktureringsstatistik till Adobe i XML-format.

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

Om du använder ett verktyg för nätverksregistrering för att övervaka statistiken för TVSDK-överföring till Adobe bör du se enheter som följande:

```
<request> 
     <sc_xml_ver>1.0</sc_xml_ver> 
     <reportSuiteID>ptebilling</reportSuiteID> 
     <visitorID>5536C629-5EF7-4F02-8E5D-9FA136CB3CED</visitorID> 
     <pageName>com.adobe.primetime.psdksample</pageName> 
     <timestamp>2016-11-22T18:06:30+0000</timestamp> 
     <userAgent>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</userAgent> 
     <contextData> 
         <billingMetrics> 
                 <contentDuration>1799111</contentDuration> 
                 <contentURL>https%3A%2F%2Fdevimages.apple.com.edgekey.net%2Fstreaming%2Fexamples%2Fbipbop_16x9%2Fbipbop_16x9_variant.m3u8</contentURL> 
                 <contentType>vod</contentType> 
                 <midrollEnabled>true</midrollEnabled> 
                 <tvsdkVersion>1.0.211</tvsdkVersion> 
                 <platform>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</platform> 
                 <publisherID>com.adobe.primetime.psdksample</publisherID> 
                 <adsEnabled>true</adsEnabled> 
                 <type>start</type> 
         </billingMetrics> 
     </contextData> 
</request>
```

De booleska egenskaperna `drmProtected`, `adsEnabled` och `midrollEnabled` visas bara om de är sanna.