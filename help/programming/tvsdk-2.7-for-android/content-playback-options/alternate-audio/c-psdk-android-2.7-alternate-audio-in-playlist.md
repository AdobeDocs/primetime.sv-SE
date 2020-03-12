---
description: Spelningslistan för en video kan ange ett obegränsat antal alternativa ljudspår för huvudvideoinnehållet. Du kanske vill lägga till olika språk i videoinnehållet eller tillåta användaren att växla mellan olika spår på sin enhet medan innehållet spelas upp.
seo-description: Spelningslistan för en video kan ange ett obegränsat antal alternativa ljudspår för huvudvideoinnehållet. Du kanske vill lägga till olika språk i videoinnehållet eller tillåta användaren att växla mellan olika spår på sin enhet medan innehållet spelas upp.
seo-title: Alternativa ljudspår i spellistan
title: Alternativa ljudspår i spellistan
uuid: 47289392-ae4e-44b9-8d54-6ccee8fe1446
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Alternativa ljudspår i spellistan {#alternate-audio-tracks-in-the-playlist}

Spelningslistan för en video kan ange ett obegränsat antal alternativa ljudspår för huvudvideoinnehållet. Du kanske vill lägga till olika språk i videoinnehållet eller tillåta användaren att växla mellan olika spår på sin enhet medan innehållet spelas upp.

Med alternativa ljudspår kan användare växla mellan flera språkspår för HTTP-videoströmmar (live/linear och VOD), och du behöver inte ändra, duplicera eller paketera om videon för varje ljudspår. Du kan ange flera språkspår för en videoresurs före eller efter resursens inledande paketering.

>[!IMPORTANT]
>
>För att det alternativa ljudet ska kunna blandas med huvudmediets videospår måste det alternativa spårets tidsstämplar matcha tidsstämplarna för ljudet i huvudspåret.

Huvudljudspåret ingår i ljudspårssamlingen med `default` etiketten. Metadata för de alternativa ljudströmmarna finns med i spellistan i `#EXT-X-MEDIA` -taggarna med `TYPE=AUDIO`.

Ett M3U8-manifest som anger flera alternativa ljudströmmar kan till exempel se ut så här:

```
#EXTM3U
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 1",
 AUTOSELECT=YES,DEFAULT=YES
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="bipbop_audio",LANGUAGE="eng",NAME="BipBop Audio 2",
 AUTOSELECT=NO,DEFAULT=NO,URI="alternate_audio_aac/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="eng",URI="subtitles/eng/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English (Forced)",DEFAULT=YES,
 AUTOSELECT=YES,FORCED=YES,LANGUAGE="eng",URI="subtitles/eng_forced/prog_index.m3u8"
#EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="Français",AUTOSELECT=YES,FORCED=NO,
 LANGUAGE="fra",URI="subtitles/fra/prog_index.m3u8"
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=263851,CODECS="mp4a.40.2, avc1.4d400d",
 RESOLUTION=416x234,AUDIO="bipbop_audio",SUBTITLES="subs" 
gear1/prog_index.m3u8
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=577610,CODECS="mp4a.40.2, avc1.4d401e",
 RESOLUTION=640x360,AUDIO="bipbop_audio",SUBTITLES="subs"
gear2/prog_index.m3u8
...
```

