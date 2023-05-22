---
title: Säker annonsinläsning över HTTPS
description: Säker annonsinläsning över HTTPS
copied-description: true
exl-id: d43418e9-631b-4344-a5b3-0a6154a325d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
