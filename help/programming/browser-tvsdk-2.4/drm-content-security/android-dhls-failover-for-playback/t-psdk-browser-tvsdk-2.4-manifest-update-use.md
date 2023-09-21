---
description: Du kan aktivera den här funktionen och söka efter relaterade händelser.
title: Använd uppdatering av mastermanifest live
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Använd uppdatering av mastermanifest live{#use-live-master-manifest-update}

Du kan aktivera den här funktionen och söka efter relaterade händelser.

1. Om du vill aktivera uppdateringar av mastermanifestet anger du uppdateringsfrekvensen (i minuter) genom att ange `NetworkConfiguration.masterUpdateInterval` -egenskap.
1. Du kan också spåra lyckade manifestuppdateringar genom att avlyssna `MediaPlayerItemEvent.MASTER_UPDATED` -händelse.
