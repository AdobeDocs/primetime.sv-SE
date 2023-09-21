---
title: Säker annonsinläsning över HTTPS
description: Säker annonsinläsning över HTTPS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---

# Säker annonsinläsning över HTTPS{#secure-ad-loading-over-https}

Adobe Primetime kan begära annonsservrar från tredje part över https även om spelaren finns på http. Endast de annonsserveranrop uppgraderas till https som klienten söker under lösningsfasen för Auditude Ad.

>[!NOTE]
>
>Den här funktionen stöds inte för Flash.

Använd följande för att aktivera säker annonsinläsning. Den är inte aktiverad som standard.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
