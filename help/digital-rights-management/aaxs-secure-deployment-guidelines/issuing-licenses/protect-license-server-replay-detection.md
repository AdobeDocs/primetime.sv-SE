---
title: Uppspelningsskydd
description: Uppspelningsskydd
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Uppspelningsskydd{#replay-protection}

Uppspelningsskydd förhindrar en angripare från att spela upp ett licensförfrågningsmeddelande och kan potentiellt orsaka en denial of service-attack (DoS) mot klienten (A *denial of service* attack är ett försök från angripare att förhindra att legitima användare av en tjänst använder tjänsten.) En repetitionsattack med återställningsräknaren kan till exempel användas för att&quot;lura&quot; licensservern att tänka på att DRM-klienten återställer sitt tillstånd, vilket leder till att kontot avbryts.

Mer information om uppspelningsskydd finns i `AbstractRequestMessage.getMessageId()` den *API-referens för Adobe Access*.
