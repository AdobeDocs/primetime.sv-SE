---
description: Du kan aktivera den här funktionen och söka efter relaterade händelser.
seo-description: Du kan aktivera den här funktionen och söka efter relaterade händelser.
seo-title: Använd överordnad manifestuppdatering live
title: Använd överordnad manifestuppdatering live
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# Använd live överordnad-manifestuppdatering{#use-live-master-manifest-update}

Du kan aktivera den här funktionen och söka efter relaterade händelser.

1. Om du vill aktivera överordnad manifestuppdateringar anger du uppdateringsfrekvensen (i minuter) genom att ange egenskapen `NetworkConfiguration.masterUpdateInterval`.
1. Du kan även spåra lyckade manifestuppdateringar genom att avlyssna händelsen `MediaPlayerItemEvent.MASTER_UPDATED`.
