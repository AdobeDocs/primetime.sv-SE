---
description: Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta webbläsare-TVSDK att lyssna efter annonsrelaterade händelser.
seo-description: Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta webbläsare-TVSDK att lyssna efter annonsrelaterade händelser.
seo-title: Visa banners
title: Visa banners
uuid: aabc126e-b3aa-42dd-ab50-a7db8e324c50
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Visa banners {#display-banner-ads}

Om du vill visa bannerannonser måste du skapa bannerinstanser och tillåta webbläsare-TVSDK att lyssna efter annonsrelaterade händelser.

Webbläsarens TVSDK innehåller en lista över bannerannonser som är kopplade till en linjär annons via `AdobePSDK.PSDKEventType.AD_STARTED` händelsen.

Manifester kan ange banners för följeslagare genom att:

* Ett HTML-fragment
* URL:en för en iFrame-sida
* URL:en för en statisk bild eller en Adobe Flash SWF-fil

Webbläsare-TVSDK anger vilka typer som är tillgängliga för ditt program för varje kompletterande annons.

Lägg till en avlyssnare för händelsen `AdobePSDK.PSDKEventType.AD_STARTED` som utför följande:
1. Rensar befintliga annonser i banderollinstansen.
1. Hämtar listan över följeslagarannonser från `Ad.getCompanionAssets`.
1. Om listan med följesedlar inte är tom kan du iterera över listan för banderollinstanser.

   Varje banner-instans (an `AdBannerAsset`) innehåller information, t.ex. bredd, höjd, resurstyp (html, iframe eller static) och data som krävs för att visa den tillhörande bannern.
1. Om en videoannons inte har några följeslagare bokade med sig innehåller listan med följesedlar inga data för den videoannonsen.
1. Skickar banderollinformationen till en funktion på sidan som visar banderollerna på lämplig plats.

   Detta är vanligtvis en `div`stil, och funktionen använder `div ID` för att visa banderollen. Exempel:

   Lägg till händelseavlyssnaren:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementera avlyssnarhanteraren:

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void 
   { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
            for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
                } 
            } 
        }  
        //...        
   }
   ```

   Exempel på JavaScript som ska hantera visningen:

   ```js
   function displayCompanion (resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
       var bannerDiv = document.getElementById('banner' + width + 'x' + height);  
   
       // Assuming that there is an HTML element on the page  
       // with an id of "banner300x250", for example 
       if (bannerDiv !== null) { 
           bannerDiv.innerHTML = data; 
       } 
   }
   ```

