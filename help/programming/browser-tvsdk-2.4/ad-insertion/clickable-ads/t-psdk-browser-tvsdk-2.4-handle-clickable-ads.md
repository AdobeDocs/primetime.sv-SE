---
description: MediaPlayer har en notifyClick()-funktion som skickar annonsrelaterade händelser när en klickbar annons spelas upp. Dessa händelser tillhandahåller annons- och annonsinformation som appen kan använda för att tillhandahålla klickfunktioner.
title: Hantera klickbara annonser
exl-id: 25738592-f3fe-4f13-b2bb-26a5f942cd18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Hantera klickbara annonser {#handle-clickable-ads}

MediaPlayer har en notifyClick()-funktion som skickar annonsrelaterade händelser när en klickbar annons spelas upp. Dessa händelser tillhandahåller annons- och annonsinformation som appen kan använda för att tillhandahålla klickfunktioner.

MediaPlayer utlöser följande händelser när en klickbar annons spelas upp:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

The `AdClickedEvent` innehåller den information som behövs för att bearbeta genomklickningsfunktionen.

1. Ge användarna en kontroll i spelaren så att de kan klicka på klickbara annonser.

   Detta kan vara en knapp eller något annat element som kan fånga användarens klickning.
1. Lägg till en händelseavlyssnare för användarens händelse för att markera och klicka.

   Till exempel:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. Lägg till en hanterare för användarens click-händelse.

   Hanteraren måste uppmana MediaPlayer att starta `AdClicked` -händelse.

   ```
   onAdClick = function (event) { 
       // Get a reference to your player 
       var player = getPlayer(); 
       if (player) { 
           // Call the MediaPlayer's notifyClick function 
           // which gets MediaPlayer to fire AdClicked 
           player.notifyClick(); 
       } 
   } 
   ```

1. Lägg till händelseavlyssnare för MediaPlayer och starta, och klicka på dem samt lägg till slutförda meddelanden.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Lägg till händelsehanterare.
a. Hantera annonsens starthändelse.
Detta kan göra vad som helst, till exempel att konfigurera användargränssnittet.

   ```
   onAdStarted = function (event) { 
       if (clickAddButton && event && event.ad) { 
           var adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           if (adClick && adClick.isValid) { 
               // Do some initial processing  
               // when the ad starts, prior 
               // to the user's click. 
           } 
       } 
   }
   ```

   b. Hantera händelsen där annonsen klickades.
I det här exemplet hämtar vi annonsinformation från händelsen och öppnar ett nytt webbläsarfönster med den informationen:

   ```
   onAdClickedEvent = function (event) { 
       if (event && event.ad) { 
           var adClick = event.adClick; 
           if (!(adClick && adClick.isValid)) { 
               adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           } 
           if (adClick && adClick.isValid) 
           { 
               // Do something with the currently playing ad 
               window.open(adClick.url); 
           } 
       } 
   }
   ```

   c. Hantera händelsen annons klar.

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
