---
description: Du kan använda ExpressPlays Bento4-paketerare för att förbereda innehåll för alla DRM-lösningar som stöds av Primetime Cloud DRM, som drivs av ExpressPlay.
title: ExpressPlay Packager / Cloud DRM / TVSDK
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

Du kan använda ExpressPlays Bento4-paketerare för att förbereda innehåll för alla DRM-lösningar som stöds av Primetime Cloud DRM, som drivs av ExpressPlay.

I den här uppgiften beskrivs hur du använder ett verktyg från tredje part för att förbereda skyddat innehåll, i det här fallet *ExpressPlay Bento4 Tools*, för användning med en mängd olika DRM-lösningar. Mer information finns i *Bento4-verktyg* dokumentation om [ExpressPlay](https://www.expressplay.com/developer/) webbplats.
1. Skaffa ett ExpressPlay-konto och få din ExpressPlay-kundautentiseringsinformation.

   Se [Primetime DRM Cloud Quick-start.](../../quick-start/quick-overview.md)
1. Om du krypterar innehåll för Primetime Access måste du skaffa Primetime Adobe Access SDK från Adobe, tillsammans med de certifikat som krävs (licens-, transport- och paketeringscertifikat).
1. Ange en innehållskrypteringsnyckel (CEK) och Content Encryption Key Storage ID (CEKSID) för användning i alla DRM-system. (Du genererar dessa slumpmässigt med OpenSSL eller liknande.)

   CEK är den faktiska nyckeln som du använder för att kryptera dina videofiler. Du kan antingen lagra den säkert på din egen server i ditt eget nyckelhanteringssystem eller använda ExpressPlay [nyckellagringslösning](https://www.expressplay.com/developer/key-storage/).

   Ett CEKSID är identifieraren för en viss CEK. Du skickar inte (vanligtvis) krypteringsnyckeln. Om du till exempel begär en licenstoken anger du CEKSID.

1. Om du krypterar innehåll för Access använder du ditt CEK för att skapa Primetime Access-metadata som är associerade med ditt innehåll.

1. Fragmentera innehållet för att förbereda det för *Bento4 MP4DASH* verktyg.

   I det här steget kan du använda *MP4FRAGMENT* verktyg. Du behöver bara fragmentera innehållet en gång. Till exempel:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Använd *Bento4 MPDASH* för att&quot;DASH-ify&quot; och kryptera fragmenterat innehåll.

   Använd det här kommandot för att ange alla DRM-system som du vill använda och skicka in alla Primetime Access-metadata som genererats från föregående steg. Till exempel:

   ```
   /mp4dash -f  
   --use-segment-list  
   --use-segment-timeline  
   --encryption-key=<CEKSID>:<CEK>  
   --playready  
   --Widevine  
   --Widevine-header=provider:intertrust#content_id:2a  
   --primetime  
   --primetime-metadata=@AAXS.metadata 
    Fragmented.mp4 -o DASH_OUTPUT
   ```

1. Skapa en&quot;storefront server&quot;.

       Den här servern måste hantera följande åtgärder:
   
   1. Kunden väljer innehåll. Den här implementeringen måste innehålla en slutpunkt där klienter kan begära en innehållstoken för ett visst innehålls-ID.
   1. Kundberättigande
   1. Licenstoken-begäranden (ExpressPlay) från klienten ( [ExpressPlay-licensens tokenbegäran/svarsreferens](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Skapa en kund.

   Klienten bör innehålla ett anrop till din storefront-server. Adobe rekommenderar att klienten anropar butiken efter att användaren har valt visst innehåll och efter att användaren har autentiserats. Skicka sedan den token som returnerats från ExpressPlay till spelaren för att använda den för licensförfrågningar. Introduktioner till implementering av DRM-komponenten för dina spelare är här:

   * Webbläsare-TVSDK för HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Med den aktuella licenstoken kan klienten nu hämta begärande-URL:en från token och göra licensbegäran till ExpressPlay och sedan spela upp det markerade, skyddade innehållet för användaren.
