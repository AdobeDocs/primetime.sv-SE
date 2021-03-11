---
description: Använd Browser TVSDK:s biblioteksfiler i din app för att skapa en Browserify-kompatibel spelare med hjälp av UI-Framework.
title: Skapa en Browserify-kompatibel spelare med UI-Framework
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Skapa en Browserify-kompatibel spelare med hjälp av UI-Framework {#create-a-browserify-compatible-player-using-the-ui-framework}

Använd Browser TVSDK:s biblioteksfiler i din app för att skapa en Browserify-kompatibel spelare med hjälp av UI-Framework.

Exempel på Browserify-filer som ingår i TVSDK:

* [!DNL [..]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/ui-framework/build/package.json]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.js]

Om du vill skapa en Browserify-kompatibel app med UI-Framework måste du `require` de två Browserify-modulerna (tillhandahålls av Browser TVSDK) i programkoden:

1. Kräv Browserify-moduler:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Fortsätt med utvecklingen enligt beskrivningen i [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Du kan nu paketera dina appfiler med Browserify.
