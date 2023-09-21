---
description: MediaPlayerNotification innehåller information som är relaterad till spelarens status.
title: Meddelandeinnehåll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
   * `code`: En numerisk representation av meddelandet.
   * `name`: En läsbar beskrivning av meddelandet, till exempel SEEK_ERROR
   * `metadata`: Nyckel-/värdepar som innehåller relevant information om meddelandet. En nyckel med namnet `URL` tillhandahåller ett värde som är en URL som är relaterad till meddelandet.

   * `innerNotification`: En referens till en annan `MediaPlayerNotification` objekt som direkt påverkar detta meddelande.

Du kan lagra informationen lokalt för senare analys eller skicka den till en fjärrserver för loggning och grafisk representation.
