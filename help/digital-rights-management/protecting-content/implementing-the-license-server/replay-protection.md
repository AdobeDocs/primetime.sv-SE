---
seo-title: Uppspelningsskydd
title: Uppspelningsskydd
uuid: c737998a-9c33-48b4-b741-91106697d71f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Uppspelningsskydd{#replay-protection}

Om du vill kunna spela upp meddelanden kan du kontrollera om meddelandets identifierare har setts nyligen genom att ringa `RequestMessageBase.getMessageId()`. I så fall kan en angripare försöka att upprepa begäran, vilket bör nekas. Servern kan identifiera uppspelningsförsök genom att lagra en lista över nyligen visade meddelande-ID:n och kontrollera varje inkommande begäran mot den cachelagrade listan. Om du vill begränsa hur lång tid som meddelandeidentifierarna behöver lagras ringer du `HandlerConfiguration.setTimestampTolerance()`. Om den här egenskapen är inställd nekas SDK sedan en begäran som har en tidsstämpel i mer än det angivna antalet sekunder av servertiden.
