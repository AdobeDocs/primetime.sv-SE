---
seo-title: Uppspelningsskydd
title: Uppspelningsskydd
uuid: 75f2be65-b2fc-428a-b853-34a4b30960ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uppspelningsskydd{#replay-protection}

För att återuppspelningsskyddet ska fungera kan det vara klokt att kontrollera om meddelandeidentifieraren har setts nyligen genom att anropa `RequestMessageBase.getMessageId()`. I så fall kan en angripare försöka att upprepa begäran, vilket bör nekas. Servern kan identifiera uppspelningsförsök genom att lagra en lista över nyligen visade meddelande-ID:n och kontrollera varje inkommande begäran mot den cachelagrade listan. Om du vill begränsa hur lång tid som meddelandeidentifierarna måste lagras, anropar du `HandlerConfiguration.setTimestampTolerance()`. Om den här egenskapen är inställd kommer SDK att neka alla förfrågningar som innehåller en tidsstämpel som är längre än det angivna antalet sekunder av servertiden.
