---
description: Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du fick andra konfigurationsparametrar från din Adobe-representant kan du använda klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.
seo-description: Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du fick andra konfigurationsparametrar från din Adobe-representant kan du använda klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.
seo-title: Konfigurera faktureringsmått
title: Konfigurera faktureringsmått
uuid: 04d3b53e-f08c-49d0-ba42-5375f1307d2e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---


# Konfigurera faktureringsmått{#configure-billing-metrics}

Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du fick andra konfigurationsparametrar från din Adobe-representant kan du använda klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.

De flesta kunder bör använda standardkonfigurationen.

>[!IMPORTANT]
>
>Den konfiguration du anger gäller så länge mediespelaren är aktiv. När du har initierat mediespelaren kan du inte ändra konfigurationen.

Så här konfigurerar du faktureringsmått:

* Ange följande kodexempel.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   där `_player` är en instans av `AdobePSDK.MediaPlayer` och `_resource` är en instans av `AdobePSDK.MediaResource`.

