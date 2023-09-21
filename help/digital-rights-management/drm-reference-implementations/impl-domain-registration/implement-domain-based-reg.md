---
title: Implementera identitetsbaserad domänregistrering
description: Implementera identitetsbaserad domänregistrering
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
