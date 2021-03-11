---
description: Replay-skydd förhindrar en angripare från att spela upp ett licensförfrågningsmeddelande och kan potentiellt orsaka en denial of service-attack (DoS) mot klienten.
title: Uppspelningsskydd
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Uppspelningsskydd{#replay-protection}

Replay-skydd förhindrar en angripare från att spela upp ett licensförfrågningsmeddelande och kan potentiellt orsaka en denial of service-attack (DoS) mot klienten.

En DoS-attack är ett försök av angripare att förhindra legitima användare av en tjänst från att använda den tjänsten. En repetitionsattack som använder rollback-räknaren kan till exempel användas för att&quot;lura&quot; licensservern att tro att DRM-klienten har återställt sitt tillstånd, vilket leder till att kontot stängs av.

Mer information om uppspelningsskydd finns i [ AbstractRequestMessage.getMessageId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/AbstractRequestMessage.html#getMessageId()).
