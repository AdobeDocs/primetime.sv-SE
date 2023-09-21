---
description: Du kan skapa en Browserify-kompatibel spelare med JS-filer som tillhandahålls av Browser TVSDK.
title: Browserify-kompatibel spelare
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Ökning {#browserify-compatible-player-overview}

Du kan skapa en Browserify-kompatibel spelare med JS-filer som tillhandahålls av Browser TVSDK.

Webbläsarens TVSDK innehåller två Browserify-kompatibla JS-filer. Den ena är avsedd att användas med AdobePSDK-modulen, den är till för utveckling av appar utan UI-ramverket. Den andra är avsedd att användas med modulen UI-Framework. Den returnerar det PTP-namnutrymme som du använder för att skriva program med UI-Framework.

Kör följande konfigurationskommandon för att komma igång med Browserify [!DNL final.js] filer (din Browserify bundle-fil) inuti [!DNL example] kataloger under [!DNL samples/browerify/reference] och [!DNL samples/browerify/ui-framework]:

1. Navigera till [!DNL samples/browserify/reference/build].
1. Kör följande kommandon:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Navigera till [!DNL samples/browserify/ui-framework/build].
1. Kör samma kommandon som i steg 2.

När den här konfigurationen är klar kan du fortsätta skapa Browserify-kompatibla TVSDK-appar baserat på exemplen som ingår i TVSDK.
