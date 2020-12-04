---
description: Använd kommandot HTTP GET för att interagera med manifestservern.
seo-description: Använd kommandot HTTP GET för att interagera med manifestservern.
seo-title: Skicka ett kommando till manifestservern
title: Skicka ett kommando till manifestservern
uuid: e9680563-d268-406d-87ce-1521a677e9ec
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Skicka ett kommando till manifestservern {#send-a-command-to-the-manifest-server}

Använd kommandot HTTP GET för att interagera med manifestservern.

1. Skicka en `HTTP GET`-begäran för en bootstrap-URL som konstruerats med följande mönster:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **** PublisherAssetIDRequired. Utgivarens unika ID för det specifika innehållet.

* **Innehållet** URLRequired. URL för M3U8-innehållsfilen, Base64-kodad för att vara säker i manifestserverns URL. Innehålls-URL:en måste peka på en variant M3U8-fil, även om det bara finns en bithastighetsström.

* **FrågeparametrarVissa** är obligatoriska, andra är valfria. Dessa utgör den mest varierade delen av begäran. De talar om för manifestservern vilken typ av klient som begär och vad den vill att manifestservern ska göra.

   Exempel:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP vs. HTTPS-begäranden**

   Manifestservern skapar URL:er med samma HTTP-protokoll som klientens begäran. Om en spelare gör en osäker HTTP-begäran (http) returnerar manifestservern URL:er för manifest och Auditude tracking URL:er med http-protokollet. Om en spelare skapar en säker HTTP-anslutning (https), manifestserver, returneras manifest-URL:er och Auditude tracking-URL:er med https-protokollet.

   >[!NOTE]
   >
   >Manifestservern kan inte ändra protokollet (HTTP eller HTTPS) för innehållssegment (.ts) och beacons för spårning från tredje part. Du måste kontakta innehållet och tredjeparts- och annonsleverantörer för att få dem att konfigurera önskade protokoll.