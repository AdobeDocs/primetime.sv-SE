---
description: En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.
title: Klasserna MediaPlayer och MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Klasserna MediaPlayer och MediaResource {#mediaplayer-and-mediaresource-classes}

En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

TVSDK ger möjlighet att läsa in och förbereda innehåll för uppspelning med `replaceCurrentResource` metod i `MediaPlayer`. Den här metoden tar två argument, en instans av `MediaPlayerResource` och, eventuellt, en instans av `MediaPlayerItemConfig`, som du kan använda för att skicka programdefinierade anpassade parametrar.

* Mer information finns i mediaplayer-reuse-or-remove.
* Mer information om `MediaPlayerResource`, se media-resource-create
