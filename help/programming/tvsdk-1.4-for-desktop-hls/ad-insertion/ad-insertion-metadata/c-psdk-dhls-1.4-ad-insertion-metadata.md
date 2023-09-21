---
description: För att annonslösaren ska kunna fungera måste annonsleverantörer, t.ex. Adobe Primetime annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.
title: Lägg till metadata för annonsinfogning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Lägg till metadata för annonsinfogning {#ad-insertion-metadata}

För att annonslösaren ska kunna fungera måste annonsleverantörer, t.ex. Adobe Primetime annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.

TVSDK innehåller annonseringsbiblioteket Primetime. För att ditt innehåll ska innehålla annonser från Primetimes annonsserver måste ditt program tillhandahålla följande `AuditudeSettings` information:

* `mediaID`, som är en unik identifierare för den video som ska spelas upp.

  Utgivaren tilldelar medie-ID när han skickar in videoinnehåll och annonsinformation till Adobe Primetime annonsbeslutsserver. Detta ID används av Primetimes annonsbeslut för att hämta relaterad annonsinformation för videon från servern.

* Dina `zoneID`, som utses av Adobe, identifierar ditt företag eller din webbplats.
* Domänen för den tilldelade annonsservern.
* Andra målparametrar.

  Du kan inkludera dessa parametrar beroende på dina behov och annonsleverantörens behov.

## Ställ in metadata för annonsinfogning {#set-up-ad-insertion-metadata}

Använd hjälpklassen AuditudeSettings, som utökar klassen MetadataNode, för att ställa in Adobe Primetime-metadata för annonsbeslut.

>[!TIP]
>
>Adobe Primetime annonsbeslut kallades tidigare Auditude.

Reklammetadata finns i `MediaResource.metadata` -egenskap. När du startar uppspelningen av en ny video ansvarar ditt program för att ställa in rätt annonsmetadata.

1. Bygg `AuditudeSettings` -instans.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Ange Adobe Primetime annonsbeslutande mediaID, zoneID, domain och de valfria målinriktningsparametrarna.

   ```
   auditudeSettings.zoneId = "yourZoneID"; 
   auditudeSettings.mediaId = "media_identifier"; 
   auditudeSettings.domain = "yourAuditudeDomain"; 
   var targetingInfo:Metadata = new Metadata(); 
   targetingInfo.setValue("yourParamName", "yourParamValue"); 
   auditudeSettings.targetingInfo = targetingInfo;
   ```

   >[!TIP]
   >
   >Medie-ID används av TVSDK som en sträng, som konverteras till ett md5-värde och används för `u` i Primetimes URL-begäran för annonsbeslut. Till exempel:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Skapa en `MediaResource` -instans med medieströmmens URL och de annonseringsmetadata som skapats tidigare.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Läs in `MediaResource` genom `MediaPlayer.replaceCurrentResource` -metod.

   The `MediaPlayer` börjar läsa in och bearbeta medieströmmens manifest.

1. (Valfritt) Fråga `MediaPlayerItem` -instans för att se om strömmen är aktiv, oavsett om den har alternativa ljudspår eller om den är skyddad.

   Den här informationen kan hjälpa dig att förbereda användargränssnittet för uppspelningen. Om du till exempel vet att det finns två ljudspår kan du inkludera en gränssnittskontroll som växlar mellan dessa spår.

1. Utlysning `MediaPlayer.prepareToPlay` för att starta annonsarbetsflödet.

   När annonserna har lösts och placerats på tidslinjen är `MediaPlayer` övergångar till tillståndet PREPARED.
1. Utlysning `MediaPlayer.play` för att starta uppspelningen.

TVSDK inkluderar nu annonser när era medier spelas upp.
