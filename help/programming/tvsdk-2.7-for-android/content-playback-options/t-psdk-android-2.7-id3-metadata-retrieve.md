---
description: ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. TVSDK identifierar ID3-taggar på segmentnivån för transportströmmen (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.
seo-description: ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. TVSDK identifierar ID3-taggar på segmentnivån för transportströmmen (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.
seo-title: ID3-taggar
title: ID3-taggar
uuid: 3fa199cd-668d-4d26-928f-074b6114b84c
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# ID3-taggar {#id-tags}

ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. TVSDK identifierar ID3-taggar på segmentnivån för transportströmmen (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.

>[!IMPORTANT]
>
>TVSDK känner igen ID3-metadata (version 2.3.0 eller 2.4.0) i ljud- (AAC) och videoströmmar (H.264) i någon av dess möjliga kodningar (ASCII, UTF8, UTF16-BE eller UTF16-LE). Den ignorerar ID3-taggar som inte finns i någon av de godkända versionerna eller formaten. Ospecificerad kodning behandlas som UTF8.

När TVSDK identifierar ID3-metadata skickas ett meddelande med följande data:

* TYPE = ID3
* NAME = ID3

1. Implementera en händelseavlyssnare för `MediaPlayer.TimedMetadataEventListener#onTimedMetadata(TimeMetadata timeMetadata)` och registrera den med objektet `MediaPlayer`.

   TVSDK anropar den här avlyssnaren när den identifierar `ID3`-metadata.

   >[!TIP]
   >
   >Anpassade annonsinställningar använder samma `onTimedMetadata`-händelse för att ange identifiering av en ny tagg. Detta bör inte skapa någon förvirring eftersom anpassade annonser identifieras på manifestnivå och ID3-taggar bäddas in i strömmen. Mer information finns i [Egna taggar](../../tvsdk-2.7-for-android/ad-insertion/custom-tags-configure/c-psdk-android-2.7-custom-tags-configure.md).


1. Hämta metadata.

   ```java
   @Override 
    public void onTimedMetadata(TimedMetadata timedMetadata) { 
       TimedMetadata.Type type = timedMetadata.getType(); 
       if (type.equals(TimedMetadata.Type.ID3)){ 
           long time = timeMetadata.getTime(); 
           Metadata metadata = timedMetadata.getMetadata(); 
           Set<String> keys = metadata.keySet(); 
           for (String key : keys){ 
               byte[] value = metadata.getByteArray(key); 
           } 
       } 
   }
   ```

