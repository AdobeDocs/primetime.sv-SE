---
title: Säker annonsinläsning över HTTPS
description: Säker annonsinläsning över HTTPS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Säker annonsinläsning över HTTPS{#secure-ad-loading-over-https}

Adobe Primetime kan begära annonsservrar från tredje part över https även om spelaren finns på http. Endast de annonsserveranrop uppgraderas till https som klienten söker under Auditude Ad-lösningsfasen.

>[!NOTE]
>
>Den här funktionen stöds inte för Flash.

Använd följande för att aktivera säker annonsinläsning. Den är inte aktiverad som standard.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
