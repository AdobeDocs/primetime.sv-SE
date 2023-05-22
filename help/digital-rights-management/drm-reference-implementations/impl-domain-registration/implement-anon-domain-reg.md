---
title: Implementera anonym domänregistrering
description: Implementera anonym domänregistrering
copied-description: true
exl-id: 304cfe6f-0917-42ef-a49a-e6c4bc9c10d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
