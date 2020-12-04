---
description: Alternativt, eller sent, ljud kan du växla mellan tillgängliga ljudspår för ett videospår. På så sätt kan användarna välja ett språkspår när videon spelas upp.
seo-description: Alternativt, eller sent, ljud kan du växla mellan tillgängliga ljudspår för ett videospår. På så sätt kan användarna välja ett språkspår när videon spelas upp.
seo-title: Alternativt ljud
title: Alternativt ljud
uuid: 0abd727c-7036-49c5-a4b7-8945711fecc8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Alternativt ljud {#alternate-audio}

Alternativt, eller sent, ljud kan du växla mellan tillgängliga ljudspår för ett videospår. På så sätt kan användarna välja ett språkspår när videon spelas upp.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

När TVSDK skapar instansen `MediaPlayerItem` för den aktuella videon skapas ett `AudioTrack`-objekt för varje tillgängligt ljudspår. Objektet innehåller en `name`-egenskap, en sträng som vanligtvis innehåller en användaridentifierbar beskrivning av språket för det spåret. Objektet innehåller även information om huruvida det spåret ska användas som standard.

När det är dags att spela upp videon kan du be om en lista med tillgängliga ljudspår, om du vill låta användaren välja ett, och ställa in videon som ska spelas upp med det valda spåret.

Om ett ytterligare ljudspår blir tillgängligt efter att `MediaPlayerItem` har skapats aktiveras en `MediaPlayerItem.AUDIO_UPDATED`-händelse av TVSDK, även om det är sällsynt.

## Lagt till API:er {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Följande API:er har lagts till som stöd för alternativt ljud:

`hasAlternateAudio`

Om det angivna mediet har ett annat ljudspår än standardspåret returnerar den här booleska funktionen `true`. Om det inte finns något alternativt ljudspår returnerar funktionen `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const { 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

Den här funktionen returnerar en lista över alla tillgängliga ljudspår i ett visst medium.

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const { 
if (_audioTracks) { 
    out = _audioTracks; 
    out->addRef(); 
    return kECSuccess; 
    } 
    return kECDataNotAvailable; 
} 
```

`getSelectedAudioTrack`

Den här funktionen som returnerar det markerade alternativa ljudspåret och egenskaper som språk. Det automatiska valet av spår kan också extraheras.

```
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const { 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

Den här funktionen väljer ett alternativt ljudspår som ska spelas upp.

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) { 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```

