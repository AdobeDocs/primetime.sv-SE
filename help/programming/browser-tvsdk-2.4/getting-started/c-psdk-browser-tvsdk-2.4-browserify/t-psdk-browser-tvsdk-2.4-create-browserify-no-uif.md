---
description: Använd Browser TVSDK i din app för att skapa en Browserify-kompatibel spelare.
seo-description: Använd Browser TVSDK i din app för att skapa en Browserify-kompatibel spelare.
seo-title: Skapa en Browserify-kompatibel spelare utan UI-Framework
title: Skapa en Browserify-kompatibel spelare utan UI-Framework
uuid: c4315bc8-c75d-4dd9-8680-946c1197be1e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Skapa en Browserify-kompatibel spelare utan UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Använd Browser TVSDK i din app för att skapa en Browserify-kompatibel spelare.

I avsnittet [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) visas en lista med de Browser TVSDK-bibliotek som du normalt tar med när du skapar en grundläggande videospelare. Det gör du genom att lägga till `script` taggar med `src` attribut som pekar på biblioteken.

Processen skiljer sig något åt när du skapar en Browserify-kompatibel spelare. För detta använder du kommandot `require` för att inkludera [!DNL AdobePSDK.module.js] filen (tillhandahålls av webbläsarens TVSDK) i din app. Den här filen paketerar de grundläggande spelarbiblioteksfilerna i rätt beroendeordning och returnerar det `AdobePSDK` namnutrymme som du använder för att implementera funktioner för spelaren.

Browser TVSDK innehåller följande exempel på Browserify-program och build-filer i releasepaketet:

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Så här skapar du en Browserify-kompatibel videospelare:

1. Kräv den Browserify-kompatibla biblioteksfilen som returnerar `AdobePSDK` namnutrymmet:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Skapa spelaren enligt beskrivningen i [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   Steg 1 i den här uppgiften ersätter steget i de grundläggande spelarinstruktionerna där du hämtar de enskilda grundläggande spelarbiblioteken i din appfil.
Du kan nu paketera dina appfiler med Browserify.
