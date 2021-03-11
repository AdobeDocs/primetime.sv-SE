---
description: En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.
title: Klasserna MediaPlayer och MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# Klasserna MediaPlayer och MediaResource {#mediaplayer-and-mediaresource-classes}

En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

TVSDK ger möjlighet att läsa in och förbereda innehåll för uppspelning genom att använda metoden `replaceCurrentResource` i `MediaPlayer`. Den här metoden tar två argument, en instans av `MediaPlayerResource` och, eventuellt, en instans av `MediaPlayerItemConfig`, som du kan använda för att skicka programdefinierade anpassade parametrar.

* Mer information finns i [Återanvända eller ta bort en MediaPlayer-instans](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayerobjects-working-with/android-3x-mediaplayer-reuse-or-remove.md).
* Mer information om `MediaPlayerResource` finns i [Skapa en medieresurs](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-create.md).