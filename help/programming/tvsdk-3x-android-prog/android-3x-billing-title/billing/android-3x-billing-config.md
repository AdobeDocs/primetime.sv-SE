---
description: Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du fick andra konfigurationsparametrar från din Adobe-representant kan du använda klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.
title: Konfigurera faktureringsmått
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Konfigurera faktureringsmått {#configure-billing-metrics}

Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du fick andra konfigurationsparametrar från din Adobe-representant kan du använda klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.

>[!TIP]
>
>De flesta kunder bör använda standardkonfigurationen.

>[!IMPORTANT]
>
>Den konfiguration du anger gäller så länge mediespelaren är aktiv. När du har initierat mediespelaren kan du inte ändra konfigurationen.

Så här konfigurerar du faktureringsmått:

Ange följande kodexempel.

```java
MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
BillingMetricsConfiguration billingConfig = new BillingMetricsConfiguration(); 
billingConfig.setEnabled(true); 
billingConfig.setProVODBillableDurationMinutes(60); 
billingConfig.setStdVODBillableDurationMinutes(30); 
billingConfig.setLiveBillableDurationMinutes(15); 
config.setBillingMetricsConfiguration(billingConfig); 
mediaPlayer.replaceCurrentResource(mediaResource, config);
```
