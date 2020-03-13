---
seo-title: Översikt över tidsbaserade regler
title: Översikt över tidsbaserade regler
uuid: 10b7766e-3b1a-4d8a-ba15-46976aa0847d
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# Tidsbaserade regler {#time-based-rules}

Primetime DRM använder&quot;mjuk framtvingning&quot; av tidsbaserade licensbegränsningar. Om en tidsrättighet förfaller under uppspelning av en video är standardbeteendet för Primetime DRM att inte begränsa uppspelningen förrän nästa gång videoströmmen återskapas (genom anrop `Netstream.stop()` och `Netstream.play()`).

Även om mjuk tvång är standardbeteendet kan du även aktivera hård tvång genom att utföra någon av följande åtgärder:

* Be din videospelare att regelbundet avsöka licensen för att säkerställa att inga tidsbegränsningar har gått ut. Detta kan du göra genom att anropa `DRMManager.loadVoucher(LOCAL_ONLY).` En felkod anger att den lokalt lagrade licensen inte längre är giltig.
* När användaren klickar **[!UICONTROL Pause]** kan du spela in den aktuella tidsstämpeln och sedan anropa `Netstream.stop()`. När användaren klickar på uppspelningsknappen kan du söka efter den inspelade platsen och sedan ringa `Netstream.play()`.