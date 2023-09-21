---
title: Uppspelningsskydd
description: Uppspelningsskydd
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# Uppspelningsskydd{#replay-protection}

För uppspelningsskydd kan det vara klokt att kontrollera om meddelandeidentifieraren har setts nyligen genom att anropa `RequestMessageBase.getMessageId()`. I så fall kan en angripare försöka att upprepa begäran, vilket bör nekas. Servern kan identifiera uppspelningsförsök genom att lagra en lista över nyligen visade meddelande-ID:n och kontrollera varje inkommande begäran mot den cachelagrade listan. Om du vill begränsa hur lång tid som meddelandeidentifierarna behöver lagras, ringer du `HandlerConfiguration.setTimestampTolerance()`. Om den här egenskapen är inställd kommer SDK att neka alla förfrågningar som innehåller en tidsstämpel som är längre än det angivna antalet sekunder av servertiden.
