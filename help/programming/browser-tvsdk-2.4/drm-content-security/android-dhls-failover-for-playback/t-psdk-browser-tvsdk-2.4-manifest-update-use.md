---
description: Du kan aktivera den här funktionen och söka efter relaterade händelser.
seo-description: Du kan aktivera den här funktionen och söka efter relaterade händelser.
seo-title: Använd uppdatering av mastermanifest live
title: Använd uppdatering av mastermanifest live
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Använd uppdatering av mastermanifest live{#use-live-master-manifest-update}

Du kan aktivera den här funktionen och söka efter relaterade händelser.

1. Om du vill aktivera uppdateringar av mastermanifestet anger du uppdateringsfrekvensen (i minuter) genom att ange `NetworkConfiguration.masterUpdateInterval` egenskapen.
1. Du kan också spåra lyckade manifestuppdateringar genom att avlyssna `MediaPlayerItemEvent.MASTER_UPDATED` händelsen.
