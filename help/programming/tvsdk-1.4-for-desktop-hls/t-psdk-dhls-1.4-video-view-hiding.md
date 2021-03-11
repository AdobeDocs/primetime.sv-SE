---
description: När en MediaPlayer-vy har använts för att spela upp video kan du dölja den och visa den igen med en TVSDK-metod eller manuellt.
title: Dölja en videovy
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 1%

---


# Dölj en videovy{#hide-a-video-view}

När en MediaPlayer-vy har använts för att spela upp video kan du dölja den och visa den igen med en TVSDK-metod eller manuellt.

Du måste pausa en video innan du rensar den eller flyttar den från skärmen.
* Alternativ 1: Rensa videobildrutan med `MediaPlayer.clearVideo` &#x200B; och ersätt bildrutan senare.
   * Pausa videon som du vill dölja.
   * Ta bort den visade videobildrutan genom att anropa `MediaPlayer.clearVideo`.
   * Om du vill återställa `MediaPlayer` så att det kan spelas upp igen, anropar du `replaceCurrentResource` eller `replaceCurrentItem`.
* Alternativ 2: Flytta vyn `MediaPlayer` från skärmen och flytta tillbaka den senare utan att behöva ersätta den.
   * Pausa videon som du vill dölja.
   * Flytta ut vyn från scenen. Exempel:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * Om du vill visa videon igen flyttar du tillbaka vyn till scenen.
