---
description: Du kan använda ExpressPlays Bento4-paketerare för att förbereda innehåll för alla DRM-lösningar som stöds av Primetime Cloud DRM, som drivs av ExpressPlay.
seo-description: Du kan använda ExpressPlays Bento4-paketerare för att förbereda innehåll för alla DRM-lösningar som stöds av Primetime Cloud DRM, som drivs av ExpressPlay.
seo-title: ExpressPlay Packager / Cloud DRM / TVSDK
title: ExpressPlay Packager / Cloud DRM / TVSDK
uuid: 0d2f5a8d-15c4-42ba-acb8-1dc8d5bc62de
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

Du kan använda ExpressPlays Bento4-paketerare för att förbereda innehåll för alla DRM-lösningar som stöds av Primetime Cloud DRM, som drivs av ExpressPlay.

Den här uppgiften beskriver hur du använder ett verktyg från tredje part för att förbereda skyddat innehåll, i det här fallet *ExpressPlay Bento4 Tools*, för användning med en mängd olika DRM-lösningar. Mer information finns i dokumentationen för *Bento4-verktygen* på webbplatsen [ExpressPlay](https://www.expressplay.com/developer/) .
1. Skaffa ett ExpressPlay-konto och få din ExpressPlay-kundautentiseringsinformation.

   Se [Snabbstart för Primetime DRM Cloud.](../../quick-start/quick-overview.md)
1. Om du krypterar innehåll för Primetime Access måste du skaffa Primetimes Adobe Access SDK tillsammans med de certifikat som krävs (licens-, transport- och paketeringscertifikat).
1. Ange en innehållskrypteringsnyckel (CEK) och Content Encryption Key Storage ID (CEKSID) för användning i alla DRM-system. (Du genererar dessa slumpmässigt med OpenSSL eller liknande.)

   CEK är den faktiska nyckeln som du använder för att kryptera dina videofiler. Du kan antingen lagra den säkert på din egen server i ditt eget nyckelhanteringssystem eller använda ExpressPlays [nyckellagringslösning](https://www.expressplay.com/developer/key-storage/).

   Ett CEKSID är identifieraren för en viss CEK. Du skickar inte (vanligtvis) krypteringsnyckeln. Om du till exempel begär en licenstoken anger du CEKSID.

1. Om du krypterar innehåll för Access använder du ditt CEK för att skapa Primetime Access-metadata som är associerade med ditt innehåll.

1. Fragmentera innehållet för att förbereda det för *Bento4 MP4DASH* -verktyget.

   I det här steget kan du använda *MP4FRAGMENT* -verktyget. Du behöver bara fragmentera innehållet en gång. Exempel:

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. Använd *Bento4 MPDASH* -verktyget för att&quot;DASH-ify&quot; och kryptera fragmenterat innehåll.

   Använd det här kommandot för att ange alla DRM-system som du vill använda och skicka in alla Primetime Access-metadata som genererats från föregående steg. Exempel:

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
   1. Licenstoken-begäranden (ExpressPlay) från klienten ( [ExpressPlay-licenstokenbegäran/svarsreferens](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. Skapa en kund.

   Klienten bör innehålla ett anrop till din storefront-server. Adobe rekommenderar att kunden ringer butiken när användaren har valt visst innehåll och efter att användaren har autentiserats. Skicka sedan den token som returnerats från ExpressPlay till spelaren för att använda den för licensförfrågningar. Introduktioner till implementering av DRM-komponenten för dina spelare är här:

   * Webbläsare-TVSDK för HTML5
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. Med den aktuella licenstoken kan klienten nu hämta begärande-URL:en från token och göra licensbegäran till ExpressPlay och sedan spela upp det markerade, skyddade innehållet för användaren.
