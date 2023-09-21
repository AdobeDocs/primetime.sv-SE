---
description: Med alternativt ljud kan du växla mellan tillgängliga ljudspår för ett videospår. Användarna kan välja vilket språkspår de vill när videon spelas upp.
title: Alternativt ljud
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Ökning {#alternate-audio-overview}

Med alternativt ljud kan du växla mellan tillgängliga ljudspår för ett videospår. Användarna kan välja vilket språkspår de vill när videon spelas upp.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

När TVSDK skapar `MediaPlayerItem` -instans för den aktuella videon, skapar den `AudioTrack` objekt för varje tillgängligt ljudspår. Objektet innehåller en `name` -egenskap, som är en sträng som vanligtvis innehåller en användaridentifierbar beskrivning av språket i det spåret. Objektet innehåller även information om huruvida det spåret ska användas som standard. När det är dags att spela upp videon kan du be om en lista med tillgängliga ljudspår, om du vill tillåta användaren att välja ett spår och ställa in videon som ska spelas upp med det valda spåret.

>[!TIP]
>
>Om ytterligare ljudspår blir tillgängliga efter att TVSDK har skapat `MediaPlayerItem`, TVSDK utlöser en `MediaPlayerItem.AUDIO_TRACK_UPDATED` -händelse.

## Lagt till API:er {#section_87C42C30BA8C4F58A2DAB7CE07FCD3DE}

Följande API:er har lagts till som stöd för alternativt ljud:

`hasAlternateAudio`

Om det angivna mediet har ett annat ljudspår än standardspåret returnerar den här booleska funktionen `true`. Om det inte finns något alternativt ljudspår returnerar funktionen `false`.

```java
boolean hasAlternateAudio();
```

** `getAudioTracks`**

Den här funktionen returnerar en lista över alla tillgängliga ljudspår i ett visst medium.

```java
List<AudioTrack> getAudioTracks();
```

`getSelectedAudioTrack`

Den här funktionen som returnerar det markerade alternativa ljudspåret och egenskaper som språk. Det automatiska valet av spår kan också extraheras.

```java
AudioTrack getSelectedAudioTrack();
```

`selectAudioTrack`

Den här funktionen väljer ett alternativt ljudspår att spela upp.

```java
void selectAudioTrack(AudioTrack audioTrack);
```

Till exempel:

```java
private void onPrepared() { 
    // Select the AA track in PREPARED State 
    boolean hasAlternateAudio = _mediaPlayer.getCurrentItem().hasAlternateAudio(); 
    if(hasAlternateAudio) { 
        AudioTrack selectedAudioTrack =  
          _mediaPlayer.getCurrentItem().getSelectedAudioTrack(); 
 
        if (selectedAudioTrack == null) {  
            // Selecting default audio track  
            // If index is 1 it will select alternate audio track  
            selectedAudioTrack = _mediaPlayer.getCurrentItem().getAudioTracks().get(0);  
        } 
    } 
    _mediaPlayer.getCurrentItem().selectAudioTrack(selectedAudioTrack); 
} 
```
