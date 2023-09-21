---
description: Alternativt, eller sent, ljud kan du växla mellan tillgängliga ljudspår för ett videospår. På så sätt kan användarna välja ett språkspår när videon spelas upp.
title: Alternativt ljud
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Ökning {#alternate-audio-overview}

Alternativt, eller sent, ljud kan du växla mellan tillgängliga ljudspår för ett videospår. På så sätt kan användarna välja ett språkspår när videon spelas upp.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

När TVSDK skapar `MediaPlayerItem` -instans för den aktuella videon, skapar den `AudioTrack` objekt för varje tillgängligt ljudspår. Objektet innehåller en `name` -egenskap, en sträng som vanligtvis innehåller en användaridentifierbar beskrivning av språket i det spåret. Objektet innehåller även information om huruvida det spåret ska användas som standard.

När det är dags att spela upp videon kan du be om en lista med tillgängliga ljudspår, om du vill låta användaren välja ett, och ställa in videon som ska spelas upp med det valda spåret.

Om ett extra ljudspår blir tillgängligt efter att det har skapat `MediaPlayerItem`, TVSDK utlöser en `MediaPlayerItem.AUDIO_UPDATED` -händelse.

## Lagt till API:er {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Följande API:er har lagts till som stöd för alternativt ljud:

`hasAlternateAudio`

Om det angivna mediet har ett annat ljudspår än standardspåret returnerar den här booleska funktionen `true`. Om det inte finns något alternativt ljudspår returnerar funktionen `false`.

```
bool MediaPlayerItemImpl::hasAlternateAudio() const 
{ 
    return _hasAlternateAudio; 
}
```

** `getAudioTracks`**

Den här funktionen returnerar en lista över alla tillgängliga ljudspår i ett visst medium.

```
virtual PSDKErrorCode getAudioTracks(PSDKImmutableArray<AudioTrack>*& out) const 
    { 
        if (_audioTracks) 
        { 
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
PSDKErrorCode MediaPlayerItemImpl::getSelectedAudioTrack(AudioTrack &out) const 
{ 
    out = _currentAudioTrack; 
    return kECSuccess; 
}
```

`selectAudioTrack`

Den här funktionen väljer ett alternativt ljudspår att spela upp.

```
PSDKErrorCode MediaPlayerItemImpl::selectAudioTrack(const AudioTrack &audioTrack) 
{ 
    _lastPlayedAudioTrack = _currentAudioTrack; 
    if(_mediaPlayer && _mediaPlayer->_trickPlay) 
        return kECUnsupportedOperation; 
    _currentAudioTrack = audioTrack; 
    PSDKErrorCode result = kECSuccess; 
    if (_currentAudioTrack) 
    { 
        media::TimeLine* timeline = NULL; 
        if (_mediaPlayer->_fragHttpStreamer) 
            _mediaPlayer->_fragHttpStreamer->GetTimeLine(&timeline); 
        if (timeline) 
        { 
            for (int32_t i = timeline->GetFirstPeriodIndex(); i <= timeline->GetLastPeriodIndex(); i++){ 
                media::ErrorCode error = selectTrack(timeline,_mediaPlayer->_fragHttpStreamer, i, audioTrack.getName(), media::kSTTAudioIndex); 
                return _mediaPlayer->convertToPSDKError(error); 
            } 
        } 
    }   
    return result; 
}
```
