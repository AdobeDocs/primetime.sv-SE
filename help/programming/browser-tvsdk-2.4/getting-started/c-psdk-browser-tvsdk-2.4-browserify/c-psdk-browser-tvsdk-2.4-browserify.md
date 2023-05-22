---
description: Du kan skapa en Browserify-kompatibel spelare med JS-filer som tillhandahålls av Browser TVSDK.
title: Browserify-kompatibel spelare
exl-id: 3e9751d8-7a7e-465b-8d46-d07e4ccb1f5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Översikt {#browserify-compatible-player-overview}

Du kan skapa en Browserify-kompatibel spelare med JS-filer som tillhandahålls av Browser TVSDK.

Webbläsarens TVSDK innehåller två Browserify-kompatibla JS-filer. Den ena är avsedd att användas med modulen AdobePSDK. för utveckling av appar utan UI-ramverket. Den andra är avsedd att användas med modulen UI-Framework. returnerar det PTP-namnutrymme som du använder för att skriva program med UI-ramverket.

Kör följande konfigurationskommandon för att komma igång med Browserify [!DNL final.js] filer (din Browserify bundle-fil) inuti [!DNL example] kataloger under [!DNL samples/browerify/reference] och [!DNL samples/browerify/ui-framework]:

1. Navigera till [!DNL samples/browserify/reference/build].
1. Kör följande kommandon:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Navigera till [!DNL samples/browserify/ui-framework/build].
1. Kör samma kommandon som i steg 2.

När den här konfigurationen är klar kan du fortsätta skapa Browserify-kompatibla TVSDK-appar baserat på exemplen som ingår i TVSDK.
