---
description: Webbläsarens TVSDK stöder för närvarande uppspelning av strömmar där manifest och fragment inte innehåller tillägg.
seo-description: Webbläsarens TVSDK stöder för närvarande uppspelning av strömmar där manifest och fragment inte innehåller tillägg.
seo-title: Extensionslösa strömmar
title: Extensionslösa strömmar
uuid: c69ba62b-a940-4211-920d-2e559849fd6d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Extensionslösa strömmar{#extensionless-streams}

Webbläsarens TVSDK stöder för närvarande uppspelning av strömmar där manifest och fragment inte innehåller tillägg.

## Fragmentnivå {#section_0E035129501D4A77BBC14192D8A53A86}

Browser TVSDK tolkar de första byten i svaret för att identifiera innehållstypen för extensionless-fragment. Om ingen giltig innehållstyp hittas genereras ett fel i webbläsarens TVSDK.

## Manifestnivå {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

Browser TVSDK använder parametern `mediaResource.resourceType` som skickas i metoden `replaceCurrentResource` för att identifiera innehållstypen för manifest-URL:en. Mer information finns i klassen `AdobePSDK.MediaPlayer`.

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

Om `resourceType` inte anges avgör gränssnittsramverket resurstypen från resurs-URL-tillägget, som sedan skickas till metoden `replaceCurrentResource`.

>[!TIP]
>
>Om det inte finns något tillägg kontrollerar du att `resourceType` alltid skickas när en resurs läses in i gränssnittsramverket.

