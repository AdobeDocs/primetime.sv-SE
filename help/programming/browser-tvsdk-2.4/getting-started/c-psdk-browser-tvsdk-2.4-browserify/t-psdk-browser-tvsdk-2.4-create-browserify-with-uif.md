---
description: Använd Browser TVSDK:s biblioteksfiler i din app för att skapa en Browserify-kompatibel spelare med UI-Framework.
title: Skapa en Browserify-kompatibel spelare med UI-Framework
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Skapa en Browserify-kompatibel spelare med UI-Framework {#create-a-browserify-compatible-player-using-the-ui-framework}

Använd Browser TVSDK:s biblioteksfiler i din app för att skapa en Browserify-kompatibel spelare med UI-Framework.

Exempel på Browserify-filer som ingår i TVSDK:

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

Om du vill skapa en Browserify-kompatibel app med hjälp av UI-ramverket måste du `require` de två Browserify-modulerna (tillhandahålls av Browser TVSDK) i programkoden:

1. Kräv Browserify-moduler:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Fortsätt med utvecklingen enligt beskrivningen i [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Du kan nu paketera dina appfiler med Browserify.
