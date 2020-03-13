---
description: Vi använder både Bento4-paketeraren och Adobes offlinepaketeraren för att skapa krypterat DASH-innehåll. Bento4 används som okrypterat MP4-innehåll.
seo-description: Vi använder både Bento4-paketeraren och Adobes offlinepaketeraren för att skapa krypterat DASH-innehåll. Bento4 används som okrypterat MP4-innehåll.
seo-title: Paketera ditt innehåll med Bento4
title: Paketera ditt innehåll med Bento4
uuid: 88323a4e-d0b5-4a41-acec-7126d3e0c90b
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Paketera innehåll för WideVM och PlayReady {#package-for-widevine}

Vi använder både Bento4-paketeraren och Adobes offlinepaketeraren för att skapa krypterat DASH-innehåll. Bento4 används som okrypterat MP4-innehåll.

## Paketera ditt innehåll med Bento4{#package-your-content-with-bento}

Bento4-paketeraren förväntar att indata-mp4 ska förfragmenteras. Distribution av Bento4-paketeraren innehåller ett verktyg för detta.

**Anropar Bento4**

Typiska Bento4-paketeraranrop ser ut som exemplen nedan:

    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtitles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8e cd09fc0747c7c5ac215b3b
    —wide
    —wide-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;
    -o &quot;CC_300_640x33 60_DASH&quot;
>
    ./mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtitles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8e cd09fc0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;

I exemplet nedan kombineras PlayReady- och Widewin-scheman. I det här specifika fallet lägger paketeraren till både WideVM-innehållsskydd och PlayReady-innehållsskyddsinitieringsdata till DASH-utdatainnehållet.

    /mp4dash
    -f
    —use-segment-list
    —use-segment-timeline
    —subtitles
    —encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8e cd09fc0747c7c5ac215b3b
    —playready
    —playready-header=\&quot;LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\&quot;
    —wide
    —wide-header=provider:intertrust#content_id:2a &quot;CC_300_640x360.mp4&quot;
    
    
    -o &quot;CC_300_640x360_DASH&quot;¥där

Värdet för `--encryption-key` flaggan är i formatet `<base16 encoded key id>:<base16 encoded encryption key>`.

Flaggan anger att `--widevine-header=provider:intertrust#content_id:2a` paketeraren ska inkludera pssh-rutan i manifestet, som TVSDK för närvarande kräver för uppspelning.
Värdet för `-playready-header` PlayReady är att köpa licenser.

## Paketera innehållet med Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager används som okrypterat MP4-innehåll.

**Anropa Adobe Offline Packager**

Ett typiskt anrop till en Adobe offline-paketerare ser ut som anropet nedan:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -wide_key_id c595f214d84dc7ecf 31a8ebf1b7ddda5
    -wide_gift_provider intertrust
    -playready_LA_
    URLhttp://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214a d84dc7ecf31a8ebf1b7ddda5

I det här specifika fallet lägger offlinepaketeraren till både WideVM-innehållsskydd och PlayReady-innehållsskyddsinitieringsdata till DASH-utdatainnehållet. Värdet för `-key_file_path` är för en base64-kodad nyckel. Värdet av `-playready_LA_URL` är för PlayReady-licensköp.

Argumentet conf_path pekar på en konfigurationsfil som skulle innehålla följande:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Eftersom vissa Android-enheter - främst Amazon Fire TV - inte har stöd för ljuddekryptering är ljudkryptering valfritt.