---
title: Uppspelningsskydd
description: Uppspelningsskydd
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Uppspelningsskydd{#replay-protection}

För uppspelningsskydd kanske du vill kontrollera om meddelandeidentifieraren har setts nyligen genom att ringa `RequestMessageBase.getMessageId()`. I så fall kan en angripare försöka att upprepa begäran, vilket bör nekas. Servern kan identifiera uppspelningsförsök genom att lagra en lista över nyligen visade meddelande-ID:n och kontrollera varje inkommande begäran mot den cachelagrade listan. Om du vill begränsa hur lång tid som meddelandeidentifierarna behöver lagras, ringer du `HandlerConfiguration.setTimestampTolerance()`. Om den här egenskapen är inställd nekas SDK sedan en begäran som har en tidsstämpel i mer än det angivna antalet sekunder av servertiden.
