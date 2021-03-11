---
description: Du kan aktivera den här funktionen och söka efter relaterade händelser.
title: Använd överordnad manifestuppdatering live
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---


# Använd live överordnad-manifestuppdatering{#use-live-master-manifest-update}

Du kan aktivera den här funktionen och söka efter relaterade händelser.

1. Om du vill aktivera överordnad manifestuppdateringar anger du uppdateringsfrekvensen (i minuter) genom att ange egenskapen `NetworkConfiguration.masterUpdateInterval`.
1. Du kan även spåra lyckade manifestuppdateringar genom att avlyssna händelsen `MediaPlayerItemEvent.MASTER_UPDATED`.
