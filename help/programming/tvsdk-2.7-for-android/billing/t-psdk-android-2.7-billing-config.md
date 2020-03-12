---
description: Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du har fått andra konfigurationsparametrar från din Adobe Enablement-representant använder du klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.
seo-description: Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du har fått andra konfigurationsparametrar från din Adobe Enablement-representant använder du klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.
seo-title: Konfigurera faktureringsmått
title: Konfigurera faktureringsmått
uuid: d8656ab2-fdd8-4fe4-8578-a6c8ecd378e2
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Konfigurera faktureringsmått {#configure-billing-metrics}

Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du har fått andra konfigurationsparametrar från din Adobe Enablement-representant använder du klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.

>[!TIP]
>
>De flesta kunder bör använda standardkonfigurationen.

>[!IMPORTANT]
>
>Den konfiguration du anger gäller så länge mediespelaren är aktiv. När du har initierat mediespelaren kan du inte ändra konfigurationen.

Så här konfigurerar du faktureringsmått:

1. Ange följande kodexempel.

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

