---
description: En MediaResource representerar det innehåll som ska läsas in av MediaPlayer-instansen.
title: Klasserna MediaPlayer och MediaResource
exl-id: c4219dff-de75-4b8a-ad33-e0a721c38de7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
