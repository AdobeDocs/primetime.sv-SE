---
description: 'null'
seo-description: 'null'
seo-title: Säker annonsinläsning över HTTPS
title: Säker annonsinläsning över HTTPS
uuid: 10657f59-cfbf-4c75-9249-fc154952bc51
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Säker annonsinläsning över HTTPS{#secure-ad-loading-over-https}

Adobe Primetime kan begära annonsservrar från tredje part via https även om spelaren finns på http. Endast de annonsserveranrop uppgraderas till https som klienten söker under Auditude Ad-lösningsfasen.

>[!NOTE]
>
>Den här funktionen stöds inte för Flash.

Använd följande för att aktivera säker annonsinläsning. Den är inte aktiverad som standard.

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
