---
seo-title: Implementera anonym domänregistrering
title: Implementera anonym domänregistrering
uuid: 330d32fd-8c23-40f9-949b-635e5a9acc86
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
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
