---
title: Leverera innehåll
description: Leverera innehåll
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Leverera innehåll {#delivering-content}

Primetime DRM är oförändrat mot leveransmekanismen för innehållet eftersom miljön tar bort nätverkslagret och helt enkelt tillhandahåller det skyddade innehållet till Primetimes DRM-undersystem. Innehållet kan således levereras via HTTP, HTTP Dynamic Streaming, RTMP eller RTMPE, HLS osv.

Beroende på protokollet kan det dock vara krångligt att hämta det skyddade innehållets metadata ( `DRMContentData`, vanligtvis i form av en [!DNL .metadata]-fil som läses in sida vid sida). Dessa DRM-metadata krävs för att anropa ett `DRMManager`-API, till exempel förhämtning av licensen, DRM-autentisering eller anslutning till en enhetsdomän. Med RTMP/RTMPE-protokollet kan till exempel bara FLV- och F4V-data levereras till klienten via Flash Media Servern (FMS). På grund av detta måste klienten hämta metadatabloben på andra sätt. Ett alternativ för att lösa det här problemet är att lagra metadata på en HTTP-webbserver och implementera klientvideospelaren för att hämta lämpliga metadata, beroende på vilket innehåll som spelas upp.

```
private function getMetadata():void { 
    extrapolated-path-to-metadata = "https://metadatas.mywebserver.com/" + videoname; 
     var urlRequest : URLRequest =  
      new URLRequest(extrapolated-path-to-the-metadata + ".metadata");  
    var urlStream : URLStream = new URLStream();  
    urlStream.addEventListener(Event.COMPLETE, handleMetadata);  
    urlStream.addEventListener(IOErrorEvent.NETWORK_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.IO_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.VERIFY_ERROR, handleIOError);  
 
    try { 
        urlStream.load(urlRequest);  
    } catch(se:SecurityError) { 
        videoLog.text += se.toString() + "\n";  
    } catch(e:Error) { 
        videoLog.text += e.toString() + "\n";  
    } 
} 
```

