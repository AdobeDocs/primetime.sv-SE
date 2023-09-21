---
description: Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.
title: Infoga annonser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Ökning {#insert-ads-overview}

Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.

An *`ad break`* innehåller en eller flera annonser som spelas upp i sekvens. TVSDK infogar annonser i huvudinnehållet som medlemmar i en eller flera annonsbrytningar.

>[!NOTE]
>
>Om annonsen innehåller fel ignorerar TVSDK annonsen.
