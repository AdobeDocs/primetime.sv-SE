---
title: Översikt över tidsbaserade regler
description: Översikt över tidsbaserade regler
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Tidsbaserade regler {#time-based-rules}

Primetime DRM använder&quot;mjuk framtvingning&quot; av tidsbaserade licensbegränsningar. Om en tidsrättighet upphör vid uppspelning av en video är standardbeteendet för Primetime DRM att inte begränsa uppspelningen förrän nästa gång videoströmmen återskapas (genom att anropa `Netstream.stop()` och `Netstream.play()`).

Även om mjuk tvång är standardbeteendet kan du även aktivera hård tvång genom att utföra någon av följande åtgärder:

* Be din videospelare att regelbundet avsöka licensen för att säkerställa att inga tidsbegränsningar har gått ut. Detta kan uppnås genom att anropa `DRMManager.loadVoucher(LOCAL_ONLY).` En felkod anger att den lokalt lagrade licensen inte längre är giltig.
* När användaren klickar på **[!UICONTROL Pause]** kan du spela in den aktuella tidsstämpeln och sedan anropa `Netstream.stop()`. När användaren klickar på uppspelningsknappen kan du söka efter den inspelade platsen och sedan anropa `Netstream.play()`.