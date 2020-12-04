---
description: Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du fick andra konfigurationsparametrar från din Adobe-representant kan du använda klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.
seo-description: Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du fick andra konfigurationsparametrar från din Adobe-representant kan du använda klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.
seo-title: Konfigurera faktureringsmått
title: Konfigurera faktureringsmått
uuid: 340439bf-185b-4761-a481-010908842811
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '182'
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
