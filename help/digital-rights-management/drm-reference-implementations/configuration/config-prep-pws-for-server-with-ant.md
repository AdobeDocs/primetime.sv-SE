---
title: Förbered lösenord med Ant
description: Förbered lösenord med Ant
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# Förbered lösenord med Ant{#prepare-passwords-using-ant}

Använd Ant för att kryptera ditt lösenord:

1. Navigera till `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Ange `sdkdir` egenskap i [!DNL build-refimpl.xml] för att peka på den katalog som innehåller Primetime DRM Java SDK.
1. Kör följande kommando:

   ```
   ant -f build-refimpl.xml
   ```
