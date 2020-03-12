---
description: För att annonslösaren ska kunna fungera måste annonsleverantörer, som Adobe Primetime och annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.
seo-description: För att annonslösaren ska kunna fungera måste annonsleverantörer, som Adobe Primetime och annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.
seo-title: Lägg in metadata
title: Lägg in metadata
uuid: 3eb024c3-4bb5-4bee-943e-fe0c60379e60
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Lägg in metadata {#ad-insertion-metadata}

För att annonslösaren ska kunna fungera måste annonsleverantörer, som Adobe Primetime och annonsbeslut, ha konfigurationsvärden för att aktivera anslutningen till leverantören.

TVSDK innehåller annonseringsbiblioteket Primetime. För att ditt innehåll ska innehålla annonser från Primetimes annonsserver måste ditt program tillhandahålla följande obligatoriska `AuditudeSettings` information:

* `mediaID`, som är en unik identifierare för den video som ska spelas upp.

   Utgivaren tilldelar medie-ID när han skickar in videoinnehåll och annonsinformation till Adobe Primetimes annonsbeslutsserver. Detta ID används av Primetimes annonsbeslut för att hämta relaterad annonsinformation för videon från servern.

* Ditt företag `zoneID`eller din webbplats är tilldelad av Adobe.
* Domänen för den tilldelade annonsservern.
* Andra parametrar för målinriktning.

   Du kan inkludera dessa parametrar beroende på dina behov och annonsleverantörens behov.

## Ställ in metadata för annonsinfogning {#set-up-ad-insertion-metadata}

Använd hjälpklassen AuditudeSettings, som utökar klassen MetadataNode, för att ställa in metadata för Adobe Primetime-annonsbeslut.

>[!TIP]
>
>Adobe Primetimes annonsbeslut kallades tidigare Auditude.

Advertising metadata is in the `MediaResource.metadata` property. När du startar uppspelningen av en ny video ansvarar ditt program för att ställa in rätt annonsmetadata.

1. Bygg `AuditudeSettings` instansen.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Ange Adobe Primetimes annonsbeslutande mediaID, zoneID, domain och de valfria målinriktningsparametrarna.

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
   >Medie-ID används av TVSDK som en sträng, som konverteras till ett md5-värde, och används för `u` värdet i Primetimes URL-begäran om annonsbeslut. Exempel:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Skapa en `MediaResource` instans med hjälp av medieströmmens URL och de annonseringsmetadata som skapats tidigare.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Läs in `MediaResource` objektet via `MediaPlayer.replaceCurrentResource` metoden.

   Inläsningen och bearbetningen av medieströmmens manifest `MediaPlayer` påbörjas.

1. (Valfritt) Fråga `MediaPlayerItem` instansen för att se om strömmen är aktiv, oavsett om den har alternativa ljudspår eller om strömmen är skyddad.

   Den här informationen kan hjälpa dig att förbereda användargränssnittet för uppspelningen. Om du till exempel vet att det finns två ljudspår kan du inkludera en gränssnittskontroll som växlar mellan dessa spår.

1. Ring `MediaPlayer.prepareToPlay` för att starta annonsarbetsflödet.

   När annonserna har lösts och placerats på tidslinjen övergår `MediaPlayer` de till tillståndet PREPARED.
1. Anropa `MediaPlayer.play` för att starta uppspelningen.

TVSDK inkluderar nu annonser när era medier spelas upp.