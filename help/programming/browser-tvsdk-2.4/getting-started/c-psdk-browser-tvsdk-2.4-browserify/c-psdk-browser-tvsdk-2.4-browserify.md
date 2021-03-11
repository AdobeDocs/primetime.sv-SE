---
description: Du kan skapa en Browserify-kompatibel spelare med JS-filer som tillhandahålls av Browser TVSDK.
title: Browserify-kompatibel spelare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---


# Översikt {#browserify-compatible-player-overview}

Du kan skapa en Browserify-kompatibel spelare med JS-filer som tillhandahålls av Browser TVSDK.

Webbläsarens TVSDK innehåller två Browserify-kompatibla JS-filer. Den ena är avsedd att användas med modulen AdobePSDK. för utveckling av appar utan UI-ramverket. Den andra är avsedd att användas med modulen UI-Framework. returnerar det PTP-namnutrymme som du använder för att skriva program med UI-ramverket.

Om du vill komma igång med Browserify kör du följande installationskommandon för att skapa [!DNL final.js]-filer (din Browserify-paketfil) i [!DNL example]-katalogerna under [!DNL samples/browerify/reference] och [!DNL samples/browerify/ui-framework]:

1. Navigera till [!DNL samples/browserify/reference/build].
1. Kör följande kommandon:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Navigera till [!DNL samples/browserify/ui-framework/build].
1. Kör samma kommandon som i steg 2.

När den här konfigurationen är klar kan du fortsätta skapa Browserify-kompatibla TVSDK-appar baserat på exemplen som ingår i TVSDK.
