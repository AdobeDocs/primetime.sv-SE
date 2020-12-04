---
seo-title: Implementera identitetsbaserad domänregistrering
title: Implementera identitetsbaserad domänregistrering
uuid: 4a71b2e0-d1a2-4d63-9cbd-980a292774ab
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
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
