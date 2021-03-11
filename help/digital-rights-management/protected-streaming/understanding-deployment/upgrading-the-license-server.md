---
title: Uppgradera Adobe Primetime DRM Server for Protected Streaming
description: Uppgradera Adobe Primetime DRM Server for Protected Streaming
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Uppgraderar Adobe Primetime DRM-servern för skyddad direktuppspelning{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Om du vill uppgradera en server som kör Primetime DRM-servern för skyddad direktuppspelning måste du ersätta `flashaccessserver.war`-filen som har distribuerats på programservern med filen som ingår i den senaste Primetime-DRM-filen.

Om du vill använda de nya konfigurationsalternativen måste du uppdatera serverns `flashaccess-tenant.xml`. Du måste också uppdatera [!DNL jsafe.dll] eller [!DNL libjsafe.so] med den version som ingår i den senaste Primetime-DRM-modulen.
