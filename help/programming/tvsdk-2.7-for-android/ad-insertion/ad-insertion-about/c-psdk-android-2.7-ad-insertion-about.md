---
description: Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.
seo-description: Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.
seo-title: Infoga annonser
title: Infoga annonser
uuid: 7c178295-e800-4eaa-904a-45e55e70dc02
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# Översikt {#insert-ads-overview}

Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.

En *`ad break`* innehåller en eller flera annonser som spelas upp i sekvens. TVSDK infogar annonser i huvudinnehållet som medlemmar i en eller flera annonsbrytningar.

>[!NOTE]
>
>Om annonsen innehåller fel ignorerar TVSDK annonsen.