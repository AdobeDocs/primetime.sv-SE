---
seo-title: Viktiga åtgärder för videouppspelning
title: Viktiga åtgärder för videouppspelning
description: PlaybackManager tillhandahåller viktiga åtgärder för HLS-direktuppspelning
seo-description: PlaybackManager tillhandahåller viktiga åtgärder för HLS-direktuppspelning
uuid: 7ac93f1f-9233-4462-a4be-528d1aa524a9
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Viktiga åtgärder för videouppspelning {#essential-operations-of-video-playback}

PlaybackManager innehåller viktiga åtgärder för HLS-direktuppspelning:

* Anropar [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html) som kan svara på videohändelser på rätt sätt.
* Tillhandahåller uppspelningsåtgärd som uppspelning, paus och sökning.
* Returnerar information om spelaren, t.ex. spelarstatus, uppspelningsintervall och direktuppspelningsvideoflödet.
* Avgör om ABR är aktiverat och ställer in ABR- och buffertkontrollparametrar beroende på angivna konfigurationsdata.
* Avgör om buffertkontrollen är aktiverad och ställer in parametrar för buffertkontroll beroende på angivna konfigurationsdata.