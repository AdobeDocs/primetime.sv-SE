---
title: Viktiga åtgärder för videouppspelning
description: PlaybackManager tillhandahåller viktiga åtgärder för HLS-direktuppspelning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Viktiga åtgärder för videouppspelning {#essential-operations-of-video-playback}

PlaybackManager innehåller viktiga åtgärder för HLS-direktuppspelning:

* Anropar [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html) som kan svara på videohändelser på rätt sätt.
* Tillhandahåller uppspelningsåtgärd som uppspelning, paus och sökning.
* Returnerar information om spelaren, t.ex. spelarstatus, uppspelningsintervall och direktuppspelningsvideoflödet.
* Avgör om ABR är aktiverat och ställer in ABR- och buffertkontrollparametrar beroende på angivna konfigurationsdata.
* Avgör om buffertkontrollen är aktiverad och ställer in parametrar för buffertkontroll beroende på angivna konfigurationsdata.