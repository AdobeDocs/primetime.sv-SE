---
title: Förbered lösenord med Ant
description: Förbered lösenord med Ant
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 5%

---


# Förbered lösenord med Ant{#prepare-passwords-using-ant}

Använd Ant för att kryptera ditt lösenord:

1. Navigera till `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Ange egenskapen `sdkdir` i [!DNL build-refimpl.xml] för att peka på katalogen som innehåller Primetime DRM Java SDK.
1. Kör följande kommando:

   ```
   ant -f build-refimpl.xml
   ```

