---
title: Viktiga åtgärder för videouppspelning
description: PlaybackManager tillhandahåller viktiga åtgärder för HLS-direktuppspelning
exl-id: b4d1b41a-7a16-47f5-be88-6b52f0451813
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Viktiga åtgärder för videouppspelning {#essential-operations-of-video-playback}

PlaybackManager innehåller viktiga åtgärder för HLS-direktuppspelning:

* Anropar [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), som kan svara på videohändelser på rätt sätt.
* Tillhandahåller uppspelningsåtgärd som uppspelning, paus och sökning.
* Returnerar information om spelaren, t.ex. spelarstatus, uppspelningsintervall och direktuppspelningsvideoflödet.
* Avgör om ABR är aktiverat och ställer in ABR- och buffertkontrollparametrar beroende på angivna konfigurationsdata.
* Avgör om buffertkontrollen är aktiverad och ställer in parametrar för buffertkontroll beroende på angivna konfigurationsdata.
