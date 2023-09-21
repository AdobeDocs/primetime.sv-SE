---
description: Webbläsarens TVSDK stöder för närvarande uppspelning av strömmar där manifest och fragment inte innehåller tillägg.
title: Extensionslösa strömmar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Extensionslösa strömmar{#extensionless-streams}

Webbläsarens TVSDK stöder för närvarande uppspelning av strömmar där manifest och fragment inte innehåller tillägg.

## Fragmentnivå {#section_0E035129501D4A77BBC14192D8A53A86}

Browser TVSDK tolkar de första byten i svaret för att identifiera innehållstypen för extensionless-fragment. Om ingen giltig innehållstyp hittas genereras ett fel i webbläsarens TVSDK.

## Manifestnivå {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

Webbläsaren TVSDK använder `mediaResource.resourceType` parameter som skickas i `replaceCurrentResource` metod för att identifiera innehållstypen för manifest-URL. Mer information finns i `AdobePSDK.MediaPlayer` klassen.

I UI Framework Player kan du ange resurstypen i medieresursen enligt följande:

```js
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
  player: { 
    mediaResource: { 
      resourceUrl:'Specify Resource Url', 
      resourceType: ‘Specify Resource Type. Refer AdobePSDK.MediaResourceType' 
    } 
  } 
}); 
```

If `resourceType` anges inte, avgör gränssnittsramverket resurstypen från resurs-URL-tillägget, som sedan skickas till `replaceCurrentResource` -metod.

>[!TIP]
>
>Kontrollera att det inte finns något tilläggsmanifest för `resourceType` skickas alltid när en resurs läses in i gränssnittsramverket.
