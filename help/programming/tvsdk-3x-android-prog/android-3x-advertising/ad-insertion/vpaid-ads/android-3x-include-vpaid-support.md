---
description: Om du vill lägga till stöd för VPAID 2.0 lägger du till en anpassad annonsvy och lämpliga avlyssnare.
seo-description: Om du vill lägga till stöd för VPAID 2.0 lägger du till en anpassad annonsvy och lämpliga avlyssnare.
seo-title: Implementera VPAID 2.0-integrering
title: Implementera VPAID 2.0-integrering
uuid: d512fb5b-001c-4a7a-a553-d5962002bb30
translation-type: tm+mt
source-git-commit: 83df68905f74931355264661aed6cff43b802d3f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 2%

---


# Implementera VPAID 2.0-integrering {#implement-vpaid-integration}

Om du vill lägga till stöd för VPAID 2.0 lägger du till en anpassad annonsvy och lämpliga avlyssnare.

1. Lägg till den anpassade annonsvyn i spelargränssnittet när spelaren är i läget FÖRBEREDD.

   ```java
   ... 
   private FrameLayout _playerFrame; 
       ... 
       case PREPARED: 
           ... 
           addCustomView(); 
   ... 
   private void addCustomView() { 
       ... 
       WebView view = (WebView)_mediaPlayer.getCustomAdView(); 
       ... 
       _playerFrame.addView(view);
   ```

1. Skapa avlyssnare och bearbeta händelserna som beskrivs i [Händelser](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   >[!IMPORTANT]
   >
   >I ett VPAID 2.0-arbetsflöde är det mycket viktigt att behålla din `CustomAdView`-instans i alla `AdBreak` starter (event `AD_BREAK_START`) och `AdBreak` slutförs (event `AD_BREAK_COMPLETE`) från den tidpunkt du skapar den anpassade annonsvyn till den tidpunkt du tar bort den. Det innebär att du inte ska skapa en anpassad annonsvy vid varje annonsstart och ta bort den vid varje annonsbrytning.
   >
   >
   >Dessutom bör du bara skapa en anpassad annonsvy när spelaren är i läget FÖRBEREDD,
   >
   >
   >Ta bara bort den anpassade annonsvyn när återställning anropas. Exempel:
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```
   >
   >Slutligen måste du ta bort den anpassade annonsvyn från `FrameLayout` innan du tar bort den. Exempel:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
