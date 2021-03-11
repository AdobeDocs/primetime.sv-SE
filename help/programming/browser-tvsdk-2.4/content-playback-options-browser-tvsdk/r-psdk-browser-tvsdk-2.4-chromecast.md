---
description: Du kan omvandla alla strömmar från en TVSDK-baserad avsändarapp och låta strömmen spelas upp på Chromecast med Browser TVSDK.
title: Google Cast-app för webbläsare TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Google Cast-app för webbläsare TVSDK{#google-cast-app-for-browser-tvsdk}

Du kan omvandla alla strömmar från en TVSDK-baserad avsändarapp och låta strömmen spelas upp på Chromecast med Browser TVSDK.

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

Det finns två komponenter i en Cast-aktiverad app:

* Avsändarappen som fungerar som fjärrkontroll.

   Avsändarapparna innehåller smartphones, persondatorer osv. Appen kan utvecklas med systemspecifika SDK:er för iOS, Android och Chrome.
* Mottagarappen som körs på Chromecast och spelar upp innehållet.

   >[!IMPORTANT]
   >
   >Den här appen kan bara vara en HTML5-app.

Avsändaren och mottagaren kommunicerar genom att använda SDK:er för att skicka meddelanden.

## Grundläggande arbetsflöde {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

Här är en översikt över processen:

1. Avsändarappen upprättar en anslutning till mottagarappen.
1. Avsändarappen skickar ett meddelande om att läsa in media i mottagarappen.
1. Mottagarappen påbörjar uppspelningen.
1. Avsändarappen skickar kontrollmeddelanden för uppspelning, till exempel spela upp, pausa, söka, snabbspola framåt, snabbspola tillbaka, spola tillbaka, volymändring och så vidare, till mottagarappen.
1. Mottagarappen reagerar på dessa meddelanden.

## Meddelandeformat {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

Du måste definiera meddelandena så att avsändaren och mottagaren kan förstå. Här är ett exempel på ett sökmeddelande:

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

När du skickar anpassade meddelanden, till exempel sökmeddelandet via SDK:n för SDK:er, krävs ett anpassat namnutrymme för meddelanden. Här är ett exempel i JavaScript:

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## Upprättar en anslutning {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>Webbläsarens TVSDK-API:er är inte involverade när anslutningen upprättas.

För att upprätta en anslutning måste avsändaren och mottagaren utföra följande uppgifter:

* Avsändaren måste läsa dokumentationen för plattformen på [Sender App Development](https://developers.google.com/cast/docs/sender_apps).
* Mottagaren använder Cast-mottagarens API:er för att upprätta en anslutning till avsändarappen. Exempel:

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## Meddelandehantering {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

Information om hur du skickar meddelanden till mottagaren finns i dokumentationen för avsändarens plattform.

>[!IMPORTANT]
>
>Du måste inkludera det anpassade meddelandets namnutrymme, `MSG_NAMESPACE` i alla meddelanden.

För mottagarappen följer du dokumentationen för gipsmottagarens API:er.

**Exempel på ett Chrome-baserat avsändarmeddelande**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**Chrome Based Sender Event Handling**

Bind händelsehanterare till gränssnittselement som skickar meddelanden när motsvarande händelser aktiveras. Om du till exempel har en Chrome-baserad avsändarapp kan seek-händelsen skickas så här:

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**Hantering av mottagarmeddelande**

Här är ett exempel på hur sökmeddelandet ska hanteras i mottagarappen:

```js
customMessageBus.onMessage = function (event) { 
    var message = JSON.parse(event.data); 
    switch (message.type) { 
        case "seek":  
            player.seek(parseInt(message.seekTo)); 
            break; 
        //code for handling other events 
        default:  
            break; 
    } 
}; 
```

