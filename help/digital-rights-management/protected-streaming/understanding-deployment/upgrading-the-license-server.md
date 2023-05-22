---
title: Uppgraderar Adobe Primetime DRM Server for Protected Streaming
description: Uppgraderar Adobe Primetime DRM Server for Protected Streaming
copied-description: true
exl-id: 6edfba1b-46a2-4cbd-bc14-feeef1a36ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Uppgraderar Adobe Primetime DRM Server for Protected Streaming{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Om du vill uppgradera en server som kör Primetime DRM-servern för skyddad direktuppspelning måste du ersätta `flashaccessserver.war` som har distribuerats på programservern med den fil som ingår i den senaste Primetime DRM-modulen.

Om du vill använda de nya konfigurationsalternativen måste du uppdatera serverns `flashaccess-tenant.xml`. Du måste också uppdatera [!DNL jsafe.dll] eller [!DNL libjsafe.so] med den version som ingår i den senaste Primetime DRM-modulen.
