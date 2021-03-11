---
title: Uppspelningsskydd
description: Uppspelningsskydd
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Uppspelningsskydd{#replay-protection}

För uppspelningsskydd kan det vara klokt att kontrollera om meddelandeidentifieraren nyligen har setts genom att anropa `RequestMessageBase.getMessageId()`. I så fall kan en angripare försöka att upprepa begäran, vilket bör nekas. Servern kan identifiera uppspelningsförsök genom att lagra en lista över nyligen visade meddelande-ID:n och kontrollera varje inkommande begäran mot den cachelagrade listan. Om du vill begränsa hur lång tid som meddelandeidentifierarna behöver lagras ringer du `HandlerConfiguration.setTimestampTolerance()`. Om den här egenskapen är inställd kommer SDK att neka alla förfrågningar som innehåller en tidsstämpel som är längre än det angivna antalet sekunder av servertiden.
