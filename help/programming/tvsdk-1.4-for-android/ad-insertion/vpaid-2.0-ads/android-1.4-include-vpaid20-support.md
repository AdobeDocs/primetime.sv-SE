---
description: Om du vill lägga till stöd för VPAID 2.0 lägger du till en anpassad annonsvy och lämpliga avlyssnare.
title: Implementera VPAID 2.0-integrering
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# Implementera VPAID 2.0-integrering{#implement-vpaid-integration}

Om du vill lägga till stöd för VPAID 2.0 lägger du till en anpassad annonsvy och lämpliga avlyssnare.

Så här lägger du till stöd för VPAID 2.0:

1. Lägg till den anpassade annonsvyn i spelargränssnittet.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Lägg till en avlyssnare för anpassade annonshändelser.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

