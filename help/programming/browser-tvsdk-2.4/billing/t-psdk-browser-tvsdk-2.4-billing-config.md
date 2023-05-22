---
description: Om du använder standardkonfigurationen finns det inget annat du behöver göra för att aktivera eller konfigurera fakturering. Om du fick andra konfigurationsparametrar från din Adobe-representant kan du använda klassen BillingMetricsConfiguration för att ställa in dessa parametrar innan du initierar mediespelaren.
title: Konfigurera faktureringsmått
exl-id: 1eb50822-77a0-4b3a-a84c-b6082bcd1cad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
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
