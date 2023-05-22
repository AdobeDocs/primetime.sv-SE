---
description: Du kan aktivera den här funktionen och söka efter relaterade händelser.
title: Använd överordnad manifestuppdatering live
exl-id: 02cb3116-cc30-4139-841b-8d6297214b8b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Använd överordnad manifestuppdatering live{#use-live-master-manifest-update}

Du kan aktivera den här funktionen och söka efter relaterade händelser.

1. Om du vill aktivera överordnad manifestuppdateringar anger du uppdateringsfrekvensen (i minuter) genom att ange `NetworkConfiguration.masterUpdateInterval` -egenskap.
1. Du kan också spåra lyckade manifestuppdateringar genom att avlyssna `MediaPlayerItemEvent.MASTER_UPDATED` -händelse.
