---
description: Du kan aktivera FairPlay för Safari när du arbetar med Primetime DRM Cloud, som drivs av ExpressPlay.
seo-description: Du kan aktivera FairPlay för Safari när du arbetar med Primetime DRM Cloud, som drivs av ExpressPlay.
seo-title: Aktivera FairPlay för Safari HLS
title: Aktivera FairPlay för Safari HLS
uuid: 6a250a31-cc4b-4c4b-b1e9-893ee3ca5d78
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Aktivera FairPlay för Safari HLS {#enable-fairplay-for-safari-hls}

Du kan aktivera FairPlay för Safari när du arbetar med Primetime DRM Cloud, som drivs av ExpressPlay.

Kontrollera att du har följande:

* En fungerande exempelapp som kan spela upp HLS-video.

   Exempelappen måste kunna spela upp FairPlay-skyddat innehåll med licensieringen hanterad via Primetime DRM från ExpressPlay.
* Exempel på HLS-innehåll (ett M3U8-manifest) som paketerats med FairPlay-skydd.

Om du vill använda informationen här till fullo kan du lära dig mer om arbetsflöden med flera DRM från och med underavsnittet [Referensserver: Exempel på ExpressPlay Entitlement Server (SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) i Multi-DRM Workflows Guide. Läs först dokumentationen om hur du konfigurerar ditt berättigande och nyckelservern, och informationen nedan blir mycket mer användbar.
Du behöver följande objekt:

* Din *produktion* kundautentiserare från ExpressPlay
* Samma innehållsnyckel och `iv` som innehållet paketerades med.
* Platsen för det publika nyckelcertifikatet för FairPlay.

Så här ändrar du din FairPlay-/Safari-app:

1. Ange platsen för det offentliga nyckelcertifikat för FairPlay som användes i licensserverbegäran för FairPlay.

   Exempel:

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. Utför en manuell FairPlay-licens *token*-begäran till ExpressPlay för att erhålla en licenstoken-URL.

       Du kan slutföra det här steget på något av följande sätt:
   
   * Använd din egen ExpressPlay-produktionskundautentiserare.
   * Använd samma innehållsnyckel och `iv` i den här begäran som användes för att paketera innehållet som du vill spela upp.

      Kör följande kommando från gränssnittet och ersätt din ExpressPlay-kundautentiserare för att erhålla en licenstoken-URL för exempelinnehållet:

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      Svaret med licensens token-URL kommer att se ut ungefär så här:

      ```
      https://fp.service.expressplay.com:80/hms/fp/rights/? 
           ExpressPlayToken=<base64-encoded ExpressPlay token>
      ```

1. Ange en variabel med licensens token-URL från ExpressPlay.

   Exempel:

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. Ändra URL-schemat för innehållet från `skd://` till `https://` innan appen kan spela upp skyddat innehåll.

   Du måste lägga till den här URL-schemaändringen i appen innan du anropar licensservern som tillåter uppspelning.

   Protokollen måste ändras eftersom innehålls-ID, som ger åtkomst till innehållsnyckeln i nyckelhanteringssystemet, paketeras i M3U8-manifestet med `skd://`-protokollet. När spelaren är redo att hämta licensen för att spela upp det skyddade innehållet måste den först byta protokoll för att kunna kommunicera med ExpressPlay-licensservern. I exemplet nedan ändras `myServerProcessSPCPath` så att det innehåller rätt URL-schema för licensserverbegäran:

   ```js
   extractContentId(initData) {  
       contentId = arrayToString(initData); // contentId is passed up as a URI,  
                                            // from which the host must be extracted:  
       var link = document.createElement('a');  
       link.href = contentId;  
       var index = contentId.indexOf(':');  
       myServerProcessSPCPath = "https:" + contentId.substring(index+1);  
       console.log("severProcessSPCPAth = " + serverProcessSPCPath); return link.hostname;  
   }
   ```

