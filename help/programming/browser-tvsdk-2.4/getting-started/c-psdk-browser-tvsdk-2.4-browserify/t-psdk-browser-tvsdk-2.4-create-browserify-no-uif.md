---
description: Använd Browser TVSDK i din app för att skapa en Browserify-kompatibel spelare.
title: Skapa en Browserify-kompatibel spelare utan UI-Framework
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Skapa en Browserify-kompatibel spelare utan UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Använd Browser TVSDK i din app för att skapa en Browserify-kompatibel spelare.

Ämnet [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) visar en lista över de webbläsarbibliotek i TVSDK som du normalt tar med när du skapar en grundläggande videospelare. Det gör du genom att lägga till `script` taggar med `src` attribut som pekar på biblioteken.

Processen skiljer sig något åt när du skapar en Browserify-kompatibel spelare. För detta använder du `require` -kommando som innehåller [!DNL AdobePSDK.module.js] -fil (tillhandahålls av webbläsaren TVSDK) i din app. Den här filen paketerar de grundläggande spelarbiblioteksfilerna i rätt ordning och returnerar `AdobePSDK` namnutrymme som du använder för att implementera funktioner för spelaren.

Browser TVSDK innehåller följande exempel på Browserify-program och build-filer i releasepaketet:

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Så här skapar du en Browserify-kompatibel videospelare:

1. Kräver den Browserify-kompatibla biblioteksfilen som returnerar `AdobePSDK` namnutrymme:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Skapa din spelare enligt beskrivningen i [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   Steg 1 i den här uppgiften ersätter steget i de grundläggande spelarinstruktionerna där du hämtar de enskilda grundläggande spelarbiblioteken i din appfil.
Du kan nu paketera dina appfiler med Browserify.
