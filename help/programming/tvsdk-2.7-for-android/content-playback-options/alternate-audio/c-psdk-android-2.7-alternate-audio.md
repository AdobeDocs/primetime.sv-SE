---
description: Med alternativt ljud kan du växla mellan tillgängliga ljudspår för ett videospår. Användarna kan välja vilket språkspår de vill när videon spelas upp.
seo-description: Med alternativt ljud kan du växla mellan tillgängliga ljudspår för ett videospår. Användarna kan välja vilket språkspår de vill när videon spelas upp.
seo-title: Alternativt ljud
title: Alternativt ljud
uuid: 86aa5393-6a9e-49db-807b-7299e6b4ab2b
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Översikt {#alternate-audio-overview}

Med alternativt ljud kan du växla mellan tillgängliga ljudspår för ett videospår. Användarna kan välja vilket språkspår de vill när videon spelas upp.

<!--<a id="section_E4F9DC28A2944BD08B4190A7F98A8365"></a>-->

När TVSDK skapar instansen `MediaPlayerItem` för den aktuella videon skapas ett `AudioTrack`-objekt för varje tillgängligt ljudspår. Objektet innehåller en `name`-egenskap, som är en sträng som vanligtvis innehåller en användaridentifierbar beskrivning av språket för det spåret. Objektet innehåller även information om huruvida det spåret ska användas som standard. När det är dags att spela upp videon kan du be om en lista med tillgängliga ljudspår, om du vill tillåta användaren att välja ett spår och ställa in videon som ska spelas upp med det valda spåret.

>[!TIP]
>
>Om ett ytterligare ljudspår blir tillgängligt efter att TVSDK har skapat `MediaPlayerItem`, kommer TVSDK att utlösa en `MediaPlayerItem.AUDIO_TRACK_UPDATED`-händelse.

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

Den här funktionen väljer ett alternativt ljudspår som ska spelas upp.

```java
void selectAudioTrack(AudioTrack audioTrack);
```

Exempel:

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

