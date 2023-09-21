---
description: Adobe Offline Packager används som okrypterat MP4-innehåll.
title: Paketera ditt innehåll med Adobe Offline Packager
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Paketera ditt innehåll med Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

Adobe Offline Packager används som okrypterat MP4-innehåll.

**Anropar Adobe Offline Packager**

Ett typiskt anrop till en Adobe offline-paketerare ser ut som anropet nedan:

    java -jar OfflinePackager.jar -conf_path Content_PR_WV.xml -in_path &quot;Jaigo.mp4&quot;
    -out_path &quot;Jaigo_DASH&quot;
    -key_file_path &quot;Jaigo_DASH/_info/key.B64.random&quot;
    -wideVin_key_id c595f214d84dc7ecf31a8ebf1b7ddda5
    -wideVine_provider intertrust
    -playready_LA_URL
    http://pr.test.expressplay.com/playready/RightsManager.asmx
    -playready_keyid c595f214d84dc7ecf31a8ebf1b7ddda5
    -content_id c595f214d84dc7ecf31a8ebf1b7ddda5

I det här specifika fallet lägger offlinepaketeraren till både WideVM-innehållsskydd och PlayReady-innehållsskyddsinitieringsdata till DASH-utdatainnehållet. Värdet för `-key_file_path` är för en base64-kodad nyckel. Värdet för `-playready_LA_URL` är till för PlayReady-licensförvärv.

Argumentet conf_path pekar på en konfigurationsfil som skulle innehålla följande:

    &lt;config>
    &lt;frag_dur>4&lt;/frag_dur>
    &lt;target_dur>6&lt;/target_dur>
    &lt;encrypt_audio>false&lt;/encrypt_audio>
    &lt;/config>

Eftersom vissa Android-enheter - främst Amazon Fire TV - inte har stöd för ljuddekryptering är ljudkryptering valfritt.
