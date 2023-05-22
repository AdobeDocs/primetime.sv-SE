---
title: Förbered lösenord med Ant
description: Förbered lösenord med Ant
copied-description: true
exl-id: 78f00fd7-ca9c-49a9-9e4b-6d1e2daf9241
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# Förbered lösenord med Ant{#prepare-passwords-using-ant}

Använd Ant för att kryptera ditt lösenord:

1. Navigera till `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Ange `sdkdir` egenskap i [!DNL build-refimpl.xml] för att peka på katalogen som innehåller Primetime DRM Java SDK.
1. Kör följande kommando:

   ```
   ant -f build-refimpl.xml
   ```
