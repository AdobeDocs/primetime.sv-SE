---
description: Du kan ange textningsformat.
title: Exempel på bildtextformatering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '33'
ht-degree: 0%

---

# Exempel: Bildtextformatering{#examples-caption-formatting}

Du kan ange textningsformat.

## Exempel 1: Ange formatvärden explicit {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```js
// Set CC style. 
var tf = new AdobePSDK.TextFormat( 
      AdobePSDK.TextFormat.FONT_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.FONT_EDGE_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.SIZE_DEFAULT, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY; 
 mediaPlayer.CCStyle(tf);
```

>[!IMPORTANT]
>
>Webbläsaren TVSDK stöder inte teckensnittskant, fyllningsfärg eller fyllningsopacitet.
