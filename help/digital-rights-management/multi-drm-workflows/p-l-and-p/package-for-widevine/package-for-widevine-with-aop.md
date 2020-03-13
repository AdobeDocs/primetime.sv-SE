---
description: Adobe Offline Packager används som okrypterat MP4-innehåll.
seo-description: Adobe Offline Packager används som okrypterat MP4-innehåll.
seo-title: Paketera innehållet med Adobe Offline Packager
title: Paketera innehållet med Adobe Offline Packager
uuid: d0676147-c20f-49ea-93a6-9c8dbbbba992
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Paketera innehållet med Adobe Offline Packager{#package-your-content-with-adobe-offline-packager}

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
