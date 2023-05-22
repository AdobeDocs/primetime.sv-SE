---
title: Uppspelningsskydd
description: Uppspelningsskydd
copied-description: true
exl-id: 1e6ad730-b150-4e8f-9e79-e6b4fe006bf8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Uppspelningsskydd{#replay-protection}

Uppspelningsskydd förhindrar en angripare från att spela upp ett licensförfrågningsmeddelande och kan potentiellt orsaka en denial of service-attack (DoS) mot klienten (A *denial of service* attack är ett försök från angripare att förhindra legitima användare av en tjänst från att använda den tjänsten.) En repetitionsattack med återställningsräknaren kan till exempel användas för att&quot;lura&quot; licensservern att tänka på att DRM-klienten återställer sitt tillstånd, vilket leder till att kontot avbryts.

Mer information om uppspelningsskydd finns i `AbstractRequestMessage.getMessageId()` den *API-referens för Adobe Access*.
