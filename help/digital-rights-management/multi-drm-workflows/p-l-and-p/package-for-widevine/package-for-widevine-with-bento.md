---
description: Vi använder både Bento4-paketeraren och offlinepaketeraren i Adobe för att skapa krypterat DASH-innehåll. Bento4 används som okrypterat MP4-innehåll.
title: Paketera ditt innehåll med Bento4
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Paketera innehåll för WideVM och PlayReady {#package-for-widevine}

Vi använder både Bento4-paketeraren och offlinepaketeraren i Adobe för att skapa krypterat DASH-innehåll. Bento4 används som okrypterat MP4-innehåll.

## Paketera ditt innehåll med Bento4{#package-your-content-with-bento}

Bento4-paketeraren förväntar att indata-mp4 ska förfragmenteras. Distribution av Bento4-paketeraren innehåller ett verktyg för detta.

**Anropar Bento4**

Typiska Bento4-paketeraranrop ser ut som exemplen nedan:

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

```
./mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
```

I exemplet nedan kombineras PlayReady- och Widewin-scheman. I det här specifika fallet lägger paketeraren till både WideVM-innehållsskydd och PlayReady-innehållsskyddsinitieringsdata till DASH-utdatainnehållet.

```
/mp4dash
-f
--use-segment-list
--use-segment-timeline
--subtitles
--encryption-key=7cc7f0470019ac10d06bca13a580a9ff:5fa05f94e8cd09fc0747c7c5ac215b3b
--playready
--playready-header=\"LA_URL:http://pr.test.expressplay.com/playready/RightsManager.asmx\"
--widevine
--widevine-header=provider:intertrust#content_id:2a "CC_300_640x360.mp4"
-o "CC_300_640x360_DASH"
```

där

Värdet för `--encryption-key` flaggan finns i formuläret `<base16 encoded key id>:<base16 encoded encryption key>`.

The `--widevine-header=provider:intertrust#content_id:2a` anger att paketeraren ska inkludera pssh-rutan i manifestet, som TVSDK kräver för uppspelning.

Värdet för `-playready-header` är till för PlayReady-licensförvärv.

## Paketera ditt innehåll med Adobe Offline Packager {#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager används som okrypterat MP4-innehåll.

**Anropar Adobe Offline Packager**

Ett typiskt anrop till en Adobe offline-paketerare ser ut som anropet nedan:

```
java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path "Jaigo.mp4"
-out_path "Jaigo_DASH"
-key_file_path "Jaigo_DASH/_info/key.B64.random"
-widevine_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
-widevine_provider intertrust
-playready_LA_URL
http://pr.test.expressplay.com/playready/RightsManager.asmx
-playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
-content_id c595f214d84dc7ecf31a8ebf1b7ddda5
```

I det här specifika fallet lägger offlinepaketeraren till både WideVM-innehållsskydd och PlayReady-innehållsskyddsinitieringsdata till DASH-utdatainnehållet. Värdet för `-key_file_path` är för en base64-kodad nyckel. Värdet för `-playready_LA_URL` är till för PlayReady-licensförvärv.

Argumentet conf_path pekar på en konfigurationsfil som skulle innehålla följande:

```
<config>
<frag_dur>4</frag_dur>
<target_dur>6</target_dur>
<encrypt_audio>false</encrypt_audio>
</config>
```

Eftersom vissa Android-enheter - främst Amazon Fire TV - inte har stöd för ljuddekryptering är ljudkryptering valfritt.
