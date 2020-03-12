---
description: MediaPlayerNotification innehåller information som är relaterad till spelarens status.
seo-description: MediaPlayerNotification innehåller information som är relaterad till spelarens status.
seo-title: Meddelandeinnehåll
title: Meddelandeinnehåll
uuid: c2321a49-1b60-4e44-b8e2-a023b764d779
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Meddelandeinnehåll{#notification-content}

MediaPlayerNotification innehåller information som är relaterad till spelarens status.

TVSDK tillhandahåller en kronologisk lista över `MediaPlayerNotification` meddelanden. Varje anmälan innehåller följande information:

* Tidsstämpel
* Diagnostiska metadata som består av följande element:

   * skriv INFO, WARN eller ERROR
   * `code`: En numerisk representation av anmälan.
   * `name`: En beskrivning av meddelandet som kan läsas av människor, till exempel SEEK_ERROR
   * `metadata`: Nyckel-/värdepar som innehåller relevant information om meddelandet. En nyckel med namnet `URL` ger till exempel ett värde som är en URL som är relaterad till meddelandet.

   * `innerNotification`: En referens till ett annat `MediaPlayerNotification` objekt som direkt påverkar det här meddelandet.

Du kan lagra informationen lokalt för senare analys eller skicka den till en fjärrserver för loggning och grafisk representation.
