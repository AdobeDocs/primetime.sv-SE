---
seo-title: Uppspelningsskydd
title: Uppspelningsskydd
uuid: 5e6488e6-0834-4dcf-bc26-55019f5db320
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# Uppspelningsskydd{#replay-protection}

Replay-skydd förhindrar en angripare från att spela upp ett licensförfrågningsmeddelande och kan orsaka en denial of service-attack (DoS) mot klienten (en *denial of service*-attack är ett försök att förhindra att legitima användare av en tjänst använder tjänsten.) En repetitionsattack med återställningsräknaren kan till exempel användas för att&quot;lura&quot; licensservern att tänka på att DRM-klienten återställer sitt tillstånd, vilket leder till att kontot avbryts.

Mer information om uppspelningsskydd finns i `AbstractRequestMessage.getMessageId()` *API-referens för Adobe Access*.
