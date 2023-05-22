---
description: MediaPlayerNotification innehåller information som är relaterad till spelarens status.
title: Meddelandeinnehåll
exl-id: dc46f717-f08b-4d52-82ea-88107076f4fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Meddelandeinnehåll{#notification-content}

MediaPlayerNotification innehåller information som är relaterad till spelarens status.

TVSDK tillhandahåller en kronologisk lista med `MediaPlayerNotification` meddelanden. Varje anmälan innehåller följande information:

* Tidsstämpel
* Diagnostiska metadata som består av följande element:

   * skriv INFO, WARN eller ERROR
   * `code`: En numerisk representation av anmälan.
   * `name`: En beskrivning av meddelandet som kan läsas av människor, till exempel SEEK_ERROR
   * `metadata`: Nyckel-/värdepar som innehåller relevant information om meddelandet. En nyckel med namnet `URL` tillhandahåller ett värde som är en URL som är relaterad till meddelandet.

   * `innerNotification`: En referens till en annan `MediaPlayerNotification` objekt som direkt påverkar detta meddelande.

Du kan lagra informationen lokalt för senare analys eller skicka den till en fjärrserver för loggning och grafisk representation.
