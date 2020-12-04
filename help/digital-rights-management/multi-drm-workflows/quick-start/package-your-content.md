---
description: Paketera innehåll är processen att förbereda videomaterial för uppspelning på webben. Paketeringen innefattar att omvandla råvideo till manifestfiler och att eventuellt kryptera innehållet med olika DRM-lösningar för olika enheter och webbläsare.
seo-description: Paketera innehåll är processen att förbereda videomaterial för uppspelning på webben. Paketeringen innefattar att omvandla råvideo till manifestfiler och att eventuellt kryptera innehållet med olika DRM-lösningar för olika enheter och webbläsare.
seo-title: Paketera ditt innehåll
title: Paketera ditt innehåll
uuid: b9bc6104-a1ea-4ea0-a0a4-af8a606e5d47
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---


# Paketera ditt innehåll {#package-your-content}

Paketera innehåll är processen att förbereda videomaterial för uppspelning på webben. Paketeringen innefattar att omvandla råvideo till manifestfiler och att eventuellt kryptera innehållet med olika DRM-lösningar för olika enheter och webbläsare.

När du förbereder ditt innehåll kan du antingen använda offlinepaketeraren i Adobe eller andra verktyg som ExpressPlay Bento4-paketeraren. Paketerarna förbereder videon för uppspelning (t.ex. fragmentering av originalfilen och publicering) och skyddar videon med den DRM-lösning du valt (PlayReady, Widewin, FairPlay, Access osv.):

* [Adobe Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf)
* [ExpressPlay-paket](https://www.expressplay.com/developer/packaging-tools/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_web.png)

1. Paketera eller på annat sätt hämta innehåll som ska användas för att testa konfigurationen.

   En av de viktigaste punkterna att komma ihåg vid paketering är att det nyckel-ID (innehålls-ID) som du använder i det här paketeringssteget är samma som du måste ange i din efterföljande licenstokenbegäran. Nyckel-ID är det enda objekt som identifierar ditt CEK (som kan lagras i din egen nyckelhanteringsdatabas eller lagras med [ExpressPlays nyckellagringstjänst](https://www.expressplay.com/developer/key-storage/).

   >[!NOTE]
   >
   >För dem som är bekanta med Adobe Access är detta en viktig skillnad i hur de olika lösningarna fungerar. I Access bäddas licensnyckeln in i DRM-metadata och skickas fram och tillbaka med det skyddade innehållet. I de Multi-DRM-system som beskrivs här skickas inte själva licensen, utan lagras säkert och hämtas via nyckel-ID:t.

<!--<a id="example_52AF76B730174B79B6088280FCDF126D"></a>-->

Här följer ett exempel på hur du använder Adobe Offline Packager for Widewin. I Packager används en konfigurationsfil (t.ex. [!DNL widevine.xml]) som ser ut ungefär så här:

```
<config> 
<in_path>sample.mp4</in_path> 
<out_type>dash</out_type> 
<out_path>dash2</out_path> 
<drm/> 
<drm_sys>widevine</drm_sys> 
<frag_dur>4</frag_dur> 
<target_dur>6</target_dur> 
<key_file_path>keyfile.bin</key_file_path> 
<widevine_content_id>2a</widevine_content_id> 
<widevine_provider>intertrust</widevine_provider> 
<widevine_key_id>7debe705d938c76bfd886f077b8fa5f7</widevine_key_id> 
</config>
```

* `in_path` - Den här posten pekar på var källvideon finns på den lokala paketeringsdatorn.
* `out_type` - Den här posten beskriver typen av paketerade utdata, i det här fallet DASH (för WideVM-skydd i HTML5).
* `out_path` - Den plats på den lokala datorn där du vill att dina utdata ska hamna.
* `drm_sys` - Den DRM-lösning du packar för. Detta blir antingen `widevine`, `fairplay` eller `playready`.

* `frag_dur` och  `target_dur` är DASH-specifika varaktighetsposter som gäller videouppspelning.

* `key_file_path` - Det här är den plats där licensfilen finns på paketeringsdatorn som fungerar som CK (Content Encryption Key). Det är en Base-64-kodad 16-byte hex-sträng.
* `widevine_content_id` - Detta är &quot;vindrubriker&quot;. det är alltid  `2a`. (Blanda inte ihop detta med `widevine_key_id`.)

* `widevine_provider` - För våra syften ska du alltid ange det här som  `intertrust`.

* `widevine_key_id` - Detta är identifieraren för den licens som du angav i  `key_file_path` posten. Detta identifierar med andra ord nyckeln som du använder för att kryptera innehållet. Detta ID är en 16-byte HEX-sträng som du själv skapar.

Som anges i [Packager-dokumentationen](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf) skapar du en konfigurationsfil som innehåller de vanliga alternativen som du vill använda för att generera utdata. Skapa sedan utdata genom att ange specifika alternativ som kommandoradsargument.&quot; I det här fallet är vår config-fil ganska fullständig, så du kan skapa dina utdata på följande sätt:

```
java -jar OfflinePackager.jar -conf_path widevine.xml -out_path test_dash/ 
```

>[!NOTE]
>
>Kommandoradsparametrar har företräde framför konfigurationsparametrar. I det här exemplet finns allt som krävs i konfigurationsfilen, men vi har åsidosatt den utdatasökväg som angetts i konfigurationsfilen med `-out_path test_dash/`.

