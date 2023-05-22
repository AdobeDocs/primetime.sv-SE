---
description: Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.
title: Infoga annonser
exl-id: e36cbbc5-330b-4840-bf6e-2efe58a67077
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Översikt {#insert-ads-overview}

Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.

An *`ad break`* innehåller en eller flera annonser som spelas upp i sekvens. TVSDK infogar annonser i huvudinnehållet som medlemmar i en eller flera annonsbrytningar.

>[!NOTE]
>
>Om annonsen innehåller fel ignorerar TVSDK annonsen.
