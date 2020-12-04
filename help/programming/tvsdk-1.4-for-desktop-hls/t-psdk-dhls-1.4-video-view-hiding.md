---
description: När en MediaPlayer-vy har använts för att spela upp video kan du dölja den och visa den igen med en TVSDK-metod eller manuellt.
seo-description: När en MediaPlayer-vy har använts för att spela upp video kan du dölja den och visa den igen med en TVSDK-metod eller manuellt.
seo-title: Dölja en videovy
title: Dölja en videovy
uuid: 7cc02bf4-41ee-4af0-98ba-df070b50b88d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '185'
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
