---
description: När en MediaPlayer-vy har använts för att spela upp video kan du dölja den och visa den igen med en TVSDK-metod eller manuellt.
title: Dölja en videovy
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Dölja en videovy{#hide-a-video-view}

När en MediaPlayer-vy har använts för att spela upp video kan du dölja den och visa den igen med en TVSDK-metod eller manuellt.

Du måste pausa en video innan du rensar den eller flyttar den från skärmen.
* Alternativ 1: Rensa videobildrutan med `MediaPlayer.clearVideo`&#x200B; och ersätt bildrutan senare.
   * Pausa videon som du vill dölja.
   * Ta bort den visade videobildrutan genom att anropa `MediaPlayer.clearVideo`.
   * Återställ `MediaPlayer` så att det kan spelas upp igen, ringa `replaceCurrentResource` eller `replaceCurrentItem`.
* Alternativ 2: Flytta `MediaPlayer` visa utanför skärmen och flytta tillbaka den senare utan att behöva ersätta den.
   * Pausa videon som du vill dölja.
   * Flytta ut vyn från scenen. Till exempel:

     ```
     view.x = -300; 
     view.y = -300;
     ```

   * Om du vill visa videon igen flyttar du tillbaka vyn till scenen.
