---
title: Implementera identitetsbaserad domänregistrering
description: Implementera identitetsbaserad domänregistrering
copied-description: true
exl-id: e2f826a8-eea5-4d5f-ac4d-401d7a6c5373
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# Implementera identitetsbaserad domänregistrering{#implement-identity-based-domain-registration}

1. Skapa en DRM-princip med obligatorisk domänregistrering.
1. Ange serverns värd och port för domänserverns URL.

   I [!DNL .properties] fil, ange:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Gör autentisering med användarnamn och lösenord obligatorisk.

   I [!DNL .properties] fil, ange:

   ```
   policy.domain.anonymous=false 
   ```
