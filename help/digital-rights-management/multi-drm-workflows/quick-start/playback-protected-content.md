---
description: För att testa DRM-lösningen behöver du ett videoprogram som kan bearbeta just den DRM-lösning du arbetar med. Den här spelaren kan vara en exempelspelare som tillhandahålls av Adobe eller ett eget TVSDK-baserat videoprogram.
seo-description: För att testa DRM-lösningen behöver du ett videoprogram som kan bearbeta just den DRM-lösning du arbetar med. Den här spelaren kan vara en exempelspelare som tillhandahålls av Adobe eller ett eget TVSDK-baserat videoprogram.
seo-title: Spela upp skyddat innehåll
title: Spela upp skyddat innehåll
uuid: 84f73ee7-43d0-481c-a5e7-14f92169323c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# Spela upp skyddat innehåll {#playback-your-protected-content}

För att testa DRM-lösningen behöver du ett videoprogram som kan bearbeta just den DRM-lösning du arbetar med. Den här spelaren kan vara en exempelspelare som tillhandahålls av Adobe eller ett eget TVSDK-baserat videoprogram.

1. Använd licensserverns URL från det tokensvar du fick från ExpressPlay-servern för att testa om du kan spela upp skyddat innehåll.

   * **Widewin**  - Använd Widewin-svaret direkt som det kommer från din ExpressPlay-licenstokenbegäran.
   * **PlayReady**  - Hämta licensserverns URL och token från JSON-objektet som returneras från din licenstokenbegäran.
   * **FairPlay**  - Använd FairPlay-svaret direkt som du fått från din ExpressPlay-licensförfrågan.

1. Testa uppspelningen av skyddat innehåll med en egen spelare eller en befintlig Adobe-samplingsspelare.

   Ange webbadressen till det skyddade innehållet (platsen för ditt M3U8- eller MPD-manifest, beroende på vilken DRM-lösning du testar).

   Beroende på vilket gränssnitt som finns i den spelare du testar med kan du bli ombedd att ange licens-URL:en och token som separata strängar i inmatningsfält, som ett JSON-objekt som klistras in i en textruta eller som en frågeparameter i URL:en.

   Här anges några möjligheter för testspelare:

   * HTML5 Reference Player:

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * Exempel på TVSDK Player (under utveckling) -

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **Kontrollera uppspelningen när du testar konfigurationen av FairPlay:** FairPlay kräver några extra steg för uppspelning av innehåll när du använder ExpressPlay-licensservrarna. Om du använder [!DNL curl] för att testa dina anslutningar (enligt beskrivningen i [Licensiering](../../multi-drm-workflows/quick-start/handle-the-licensing.md)) måste du *redigera ditt M3U8-manifest* (ditt paketerade innehåll) enligt följande:

1. Lägg till svaret som du fick tillbaka från din licenstokenbegäran i taggen `#EXT-X-KEY:` i manifestet; och
1. Ändra protokollet för den URL:en från svaret (nu i manifestet), från `https://` till `skd://`.

   Här är ett komplett exempel på hur du testar uppspelning med FairPlay, inklusive licensieringssteget:

1. Använd FairPlay-licensens tokenbegäran för att hämta din licenstoken-URL. (Använd din egen autentisering av produktionskunder och se till att använda samma CEK och `iv` som användes för att paketera ditt FairPlay-innehåll.) Kör följande kommando för att hämta licensens token-URL för exempelinnehållet:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   Du bör få tillbaka ett svar med en licenstoken-URL som ser ut ungefär så här:

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. Ange det returnerade URL-svaret för licenstoken i ditt M3U8-manifest och *ändra schemat för licenstokens URL till* `sdk://` från `https://`. Nedan följer ett exempel på taggen #EXT-X-KEY i ditt M3U8-manifest:

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES, 
   URI="skd://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g- 
   CR1rnJKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPx 
   N5qomYsnwYSSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw", 
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1"
   ```

   >[!NOTE]
   >
   >Den föregående informationen gäller endast testning av FairPlay-konfigurationen. Det kanske inte gäller för din produktionskonfiguration, beroende på hur du konfigurerar hanteraren för FairPlay. Mer information finns i [Aktivera Apple FairPlay i iOS-program](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md).

Om videon spelas upp har du paketerat och licensierat innehållet. Om videon inte spelas upp kan du se om det finns några möjliga lösningar på dina problem på felsökningssidan.

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

Här är till exempel den del av användargränssnittet som finns i den första testspelaren som visas ovan, där du anger licensinformationen som hämtats från ExpressPlay-servern:

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
