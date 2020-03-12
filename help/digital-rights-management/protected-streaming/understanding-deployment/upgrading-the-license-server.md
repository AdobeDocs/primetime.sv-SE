---
seo-title: Uppgradera Adobe Primetime DRM-servern för skyddad direktuppspelning
title: Uppgradera Adobe Primetime DRM-servern för skyddad direktuppspelning
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Uppgradera Adobe Primetime DRM-servern för skyddad direktuppspelning{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Om du vill uppgradera en server som kör Primetime DRM-servern för skyddad direktuppspelning måste du ersätta `flashaccessserver.war` filen som har distribuerats på programservern med filen som ingår i den senaste Primetime-DRM-modulen.

Om du vill använda de nya konfigurationsalternativen måste du uppdatera serverns `flashaccess-tenant.xml`. Du måste också uppdatera [!DNL jsafe.dll] eller [!DNL libjsafe.so] med den version som ingår i den senaste Primetime DRM-modulen.
