---
title: Förbered lösenord med Java
description: Förbered lösenord med Java
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '22'
ht-degree: 0%

---

# Förbered lösenord med Java{#prepare-passwords-using-java}

Kör `ScrambleUtil.class` med Java:

1. Navigera till `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. På kommandoraden skriver du:

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```
