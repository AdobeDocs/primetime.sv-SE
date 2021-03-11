---
title: Implementera anonym domänregistrering
description: Implementera anonym domänregistrering
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

   Ange följande i din [!DNL .properties]-fil:

   ```
   policy.domain.anonymous=true 
   ```
