---
description: Om du vill lägga till stöd för VPAID 2.0 lägger du till en anpassad annonsvy och lämpliga avlyssnare.
title: Implementera VPAID 2.0-integrering
exl-id: 8a6b81e7-1034-48fc-87aa-4cb8ab305d15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Implementera VPAID 2.0-integrering {#implement-vpaid-integration}

Om du vill lägga till stöd för VPAID 2.0 lägger du till en anpassad annonsvy och lämpliga avlyssnare.

Så här lägger du till stöd för VPAID 2.0:

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

1. Skapa avlyssnare och bearbeta de händelser som beskrivs i händelseavlyssnare.

   >[!IMPORTANT]
   >
   >I ett VPAID 2.0-arbetsflöde är det mycket viktigt att du behåller din `CustomAdView` instans tvärs över `AdBreak` startar (händelse `AD_BREAK_START`) och `AdBreak` complete (event `AD_BREAK_COMPLETE`), från det att du skapar den anpassade annonsvyn till när du tar bort den. Det innebär att du inte ska skapa en anpassad annonsvy vid varje annonsstart och ta bort den vid varje annonsbrytning.
   >
   >
   >Dessutom bör du bara skapa en anpassad annonsvy när spelaren är i läget FÖRBEREDD,
   >
   >
   >Ta bara bort den anpassade annonsvyn när återställning anropas. Till exempel:
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >```
   >
   >Slutligen måste du ta bort den anpassade annonsvyn från `FrameLayout`. Till exempel:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
