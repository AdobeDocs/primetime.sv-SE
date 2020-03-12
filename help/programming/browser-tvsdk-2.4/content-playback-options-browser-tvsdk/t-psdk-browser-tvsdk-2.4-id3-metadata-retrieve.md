---
description: ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. Browser TVSDK identifierar ID3-taggar på segmentnivån för transportströmmar (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.
seo-description: ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. Browser TVSDK identifierar ID3-taggar på segmentnivån för transportströmmar (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.
seo-title: ID3-taggar
title: ID3-taggar
uuid: a47cd0cc-b11d-47df-b1fb-56918896ef4c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# ID3-taggar{#id-tags}

ID3-taggar ger information om en ljud- eller videofil, till exempel filens titel eller namnet på artisten. Browser TVSDK identifierar ID3-taggar på segmentnivån för transportströmmar (TS) i HLS-strömmar och skickar en händelse. Programmet kan extrahera data från taggen.

När en ny ID3-metadata hittas i den underliggande HLS-strömmen utlöses en `AdobePSDK.TimedMetadataEvent` händelse av Browser TVSDK.

Objektet `TimedMetadata` för ID3 har följande egenskaper:

<table id="table_6C61886187FB44B4B9821E4B00200018"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Egenskapsnamn </th> 
   <th colname="col2" class="entry"> Detaljer </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> type </span> </p> </td> 
   <td colname="col2"> <p>En typ av <span class="codeph"> TimedMetadata- </span> objekt. </p> <p>För ID3-metadata är värdet <span class="codeph"> AdobePSDK.TimedMetadataType.ID3 </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> tid </span> </p> </td> 
   <td colname="col2"> <p> Spelartid där tidsbestämda metadata identifierades. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> id </span> </p> </td> 
   <td colname="col2"> <p>ID för <span class="codeph"> TimedMetadata- </span> objektet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> name </span> </p> </td> 
   <td colname="col2"> <p>Namnet på <span class="codeph"> TimedMetadata- </span> objektet. För ID3-metadata är värdet"ID3". </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> innehåll </span> </p> </td> 
   <td colname="col2"> <p>Tidsbestämt metadatainnehåll. För ID3-taggar representerar det här värdet den serialiserade bytearrayen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> metadata </span> </p> </td> 
   <td colname="col2"> <p> <span class="codeph"> TimedMetadata </span> bearbetade information, som är en instans av <span class="codeph"> AdobePSDK.Metadata </span> där ID3-bildrutorna lagras. </p> <p> <p>Obs!  För Safaris <span class="codeph"> videotagg </span> visas ID3-taggens specifika bildrutedata i form av objekt via ett <span class="codeph"> AdobePSDK.Metadata- </span> objekt, medan ID3-taggens bildrutedata för andra webbläsare visas i form av en bytearray via <span class="codeph"> AdobePSDK.Metadata- </span> objektet. </p> </p> </td> 
  </tr> 
 </tbody> 
</table>

&#x200B;

De olika ID3-taggarna som lagras i `TimedMetadata` kan hämtas av programmet på följande två sätt:

* I händelseavlyssnaren AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE.

   ```
   var isSafari = function () { 
       var nAgt = navigator.userAgent; 
       var appName = navigator.appName; 
       if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
           (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
           (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
           (nAgt.indexOf('Chrome') === -1) && // is not chrome 
           (nAgt.indexOf('Safari') !== -1) //is Safari 
       ){ 
           return true; 
       } 
       return false; 
   }; 
   var hex2a = function (hex, offset, max) { 
       var str = ''; 
       if (!hex) 
           return str; 
       for (var i = offset; i < hex.length && i < offset + max; i++) 
           str += String.fromCharCode(hex[i]); 
       return str; 
   }; 
   var mediaPlayer = new AdobePSDK.MediaPlayer(); 
   mediaPlayer.addEventListener( AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE ,function(event){ 
       var td = event.timedMetadata; 
       if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
           var md = td.metadata; 
           var keySet = md.keySet; 
           var onSafari = isSafari(); 
           if(keySet && keySet.length){ 
               var msg = ''; 
               for(var j = 0; j < keySet.length; j++){ 
                   var idTag = keySet[j]; 
                   msg += idTag; 
                   if(idTag.indexOf("T") == 0){ 
                       /* text frame*/ 
                       if(onSafari){ 
                           /* text frame data is exposed in object format 
                            * where corresponding text data is exposed through 
                            * data key of text frame data object 
                            * */ 
                           var frameDataObject = md.getObject(idTag); 
                           msg += " : " + frameDataObject.data; 
                       } else { 
                           var buff = md.getByteArray(idTag); 
                           msg += " : " + hex2a(buff, 0, buff.length - 1); 
                       } 
                   } 
                   msg += " ; "; 
               } 
           } 
       } 
   }); 
   ```

* Använder `MediaPlayerItem`egenskapen `timedMetadata` .

   ```
   var isSafari = function () { 
       var nAgt = navigator.userAgent; 
       var appName = navigator.appName; 
       if ((nAgt.indexOf('MSIE') === -1) && //is not MS IE 
           (appName !== 'Netscape' || nAgt.indexOf('Trident/') === -1) && //is not MS IE11 
           (appName !== 'Netscape' || nAgt.indexOf('Edge') === -1) && // is not edge 
           (nAgt.indexOf('Chrome') === -1) && // is not chrome 
           (nAgt.indexOf('Safari') !== -1) //is Safari 
       ){ 
           return true; 
       } 
       return false; 
   }; 
   var hex2a = function (hex, offset, max) { 
       var str = ''; 
       if (!hex) 
           return str; 
       for (var i = offset; i < hex.length && i < offset + max; i++) 
           str += String.fromCharCode(hex[i]); 
       return str; 
   }; 
   var timedMetadataList = player.currentItem.timedMetadata; 
   for(var i = 0; i < timedMetadataList.length; i++){ 
       var td = timedMetadataList[i]; 
       if(td.type == AdobePSDK.TimedMetadataType.ID3){ 
           var md = td.metadata; 
           var keySet = md.keySet; 
           var onSafari = isSafari(); 
           if(keySet && keySet.length){ 
               var msg = ''; 
               for(var j = 0; j < keySet.length; j++){ 
                   var idTag = keySet[j]; 
                   msg += idTag; 
                   if(idTag.indexOf("T") == 0){ 
                       /* text frame*/ 
                       if(onSafari){ 
                           /* text frame data is exposed in object format 
                            * where corresponding text data is exposed through 
                            * data key of text frame data object 
                            * */ 
                           var frameDataObject = md.getObject(idTag); 
                           msg += " : " + frameDataObject.data; 
                       } else { 
                           var buff = md.getByteArray(idTag); 
                           msg += " : " + hex2a(buff, 0, buff.length - 1); 
                       } 
                   } 
                   msg += " ; "; 
               } 
           } 
       } 
   } 
   ```

