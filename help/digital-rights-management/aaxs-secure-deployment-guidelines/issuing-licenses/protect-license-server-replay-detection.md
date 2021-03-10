---
title: Uppspelningsskydd
description: Uppspelningsskydd
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Uppspelningsskydd{#replay-protection}

Replay-skydd förhindrar en angripare från att spela upp ett licensförfrågningsmeddelande och kan orsaka en denial of service-attack (DoS) mot klienten (en *denial of service*-attack är ett försök att förhindra att legitima användare av en tjänst använder tjänsten.) En repetitionsattack med återställningsräknaren kan till exempel användas för att&quot;lura&quot; licensservern att tänka på att DRM-klienten återställer sitt tillstånd, vilket leder till att kontot avbryts.

Mer information om uppspelningsskydd finns i `AbstractRequestMessage.getMessageId()` *API-referens för Adobe Access*.
