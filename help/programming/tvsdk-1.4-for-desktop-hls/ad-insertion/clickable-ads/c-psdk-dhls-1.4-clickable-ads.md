---
description: TVSDK ger dig information så att du kan agera på klickbara annonser. När du skapar användargränssnittet måste du bestämma hur du ska svara när en användare klickar på en klickbar annons.
seo-description: TVSDK ger dig information så att du kan agera på klickbara annonser. När du skapar användargränssnittet måste du bestämma hur du ska svara när en användare klickar på en klickbar annons.
seo-title: Klickbara annonser
title: Klickbara annonser
uuid: edefbc66-2d30-441d-9c30-256588504463
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Klickbara annonser {#clickable-ads}

TVSDK ger dig information så att du kan agera på klickbara annonser. När du skapar användargränssnittet måste du bestämma hur du ska svara när en användare klickar på en klickbar annons.

För TVSDK för Flash Runtime går det bara att klicka på linjära annonser.

## Svara på klickningar på annonser {#respond-to-clicks-on-ads}

När en användare klickar på en annons eller en relaterad knapp ansvarar ditt program för att svara. TVSDK ger dig information om mål-URL:en.

I det här exemplet visas ett sätt att hantera annonsklickningar.

1. Visa en knapp ovanpå mediespelaren varje gång en annons spelas upp. En användare som klickar på annonsen omdirigeras till annonsens URL. Den här knappen är en del av [!DNL ClickableAdsOverlay.xml].

   ```xml
      <?xml version="1.0"?> 
   <s:VGroup xmlns:fx="https://ns.adobe.com/mxml/2009"  
       xmlns:s="library://ns.adobe.com/flex/spark" percentWidth="100" horizontalAlign="center">     
           <fx:Declarations><fx:String id="text"/></fx:Declarations> 
           <s:Label text="{text}"  backgroundAlpha="0.75" backgroundColor="#DEDEDE"  
               color="#000000" paddingBottom="5" paddingRight="5" paddingLeft="5"  
               paddingTop="5"/> 
   </s:VGroup>
   ```

1. Inkludera den här övertäckningen i vårt mediespelarexempel [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. Om du vill att vyn ska vara synlig endast när en annons spelas upp avlyssnar du händelserna `onAdStart` och `onAdComplete` som skickas av .

   ```
   _player.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
   _player.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
   ```

   ```
      private function onAdStarted(event:AdPlaybackEvent):void { 
       var primaryAsset:AdAsset = event.ad.primaryAsset; 
       if (primaryAsset.adClick != null) { 
           clickableAdsOverlay.visible = true;  
       } 
   } 
   private function onAdCompleted(event:AdPlaybackEvent):void { 
       clickableAdsOverlay.visible = false; 
   }
   ```

1. Övervaka användarinteraktioner i klickbara annonser. Meddela TVSDK med `notifyClick`när användaren pekar eller klickar på annonsen eller knappen.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. Lyssna efter `AdclickEvent.AD_CLICK` händelsen.

   Om en annons spelas upp skickar TVSDK `AdClickEvent.AD_CLICK` händelsen som du kan hämta klicknings-URL:en från och relaterad information.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. Pausa mediespelaren medan användaren dirigeras till annons-URL:en.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. Visa webbadressen för annonsklickningen och relaterad information.

       Du kan till exempel visa den på något av följande sätt:
   
   * Öppna klicknings-URL:en i en webbläsare i programmet.

      På skrivbordsplattformar används video- och uppspelningsområdet vanligtvis för att anropa klicknings-URL:er när användaren klickar.
   * Dirigera om användaren till den externa webbläsaren för mobila enheter.

      På mobila enheter används video- och uppspelningsområdet för andra funktioner, som att dölja och visa kontroller, pausa uppspelning, expandera till helskärm och så vidare. På mobila enheter visas därför vanligtvis en separat vy, som en sponsorknapp, för användaren som ett sätt att starta klicknings-URL:en.

1. Stäng webbläsarfönstret där genomklickningsinformationen visas och återuppta uppspelningen av videon.
