---
title: Implementera identitetsbaserad domänregistrering
description: Implementera identitetsbaserad domänregistrering
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Implementera identitetsbaserad domänregistrering{#implement-identity-based-domain-registration}

1. Skapa en DRM-princip med obligatorisk domänregistrering.
1. Ange serverns värd och port för domänserverns URL.

   Ange följande i din [!DNL .properties]-fil:

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Gör autentisering med användarnamn och lösenord obligatorisk.

   Ange följande i din [!DNL .properties]-fil:

   ```
   policy.domain.anonymous=false 
   ```
