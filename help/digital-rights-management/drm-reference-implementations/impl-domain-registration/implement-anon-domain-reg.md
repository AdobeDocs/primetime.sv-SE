---
title: Implementera anonym domänregistrering
description: Implementera anonym domänregistrering
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# Implementera anonym domänregistrering{#implement-anonymous-domain-registration}

1. Skapa en DRM-princip som anger att domänregistrering krävs.
1. Ange domänserverns URL som:

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. Gör anonym autentisering obligatorisk.

   I [!DNL .properties] fil, ange:

   ```
   policy.domain.anonymous=true 
   ```
