---
seo-title: Leverera innehåll
title: Leverera innehåll
uuid: b277d369-fee3-4a20-9dd8-27b3a8a82a9e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Leverera innehåll {#delivering-content}

Primetime DRM är oförändrat mot leveransmekanismen för innehållet eftersom miljön tar bort nätverkslagret och helt enkelt tillhandahåller det skyddade innehållet till Primetimes DRM-undersystem. Innehållet kan således levereras via HTTP, dynamisk HTTP-strömning, RTMP eller RTMPE, HLS osv.

Beroende på protokollet kan det dock vara krångligt att hämta det skyddade innehållets metadata ( `DRMContentData` vanligtvis i form av en inläst [!DNL .metadata] fil). Dessa DRM-metadata krävs för att anropa ett `DRMManager` API, till exempel förhämtning av licensen, DRM-autentisering eller anslutning till en enhetsdomän. Med RTMP/RTMPE-protokollet kan till exempel bara FLV- och F4V-data levereras till klienten via Flash Media Server (FMS). På grund av detta måste klienten hämta metadatabloben på andra sätt. Ett alternativ för att lösa det här problemet är att lagra metadata på en HTTP-webbserver och implementera klientvideospelaren för att hämta lämpliga metadata, beroende på vilket innehåll som spelas upp.

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

