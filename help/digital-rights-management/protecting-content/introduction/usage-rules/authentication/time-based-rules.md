---
title: Tidsbaserade regler
description: Tidsbaserade regler
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Tidsbaserade regler {#time-based-rules}

Primetime DRM använder&quot;mjuk framtvingning&quot; av tidsbaserade licensbegränsningar. Om en tidsrättighet upphör vid uppspelning av en video är standardbeteendet för Primetime DRM att inte begränsa uppspelningen förrän nästa gång videoströmmen återskapas (genom att anropa `Netstream.stop()` och `Netstream.play()`).

Även om mjuk tvång är standardbeteendet kan du även aktivera hård tvång genom att utföra någon av följande åtgärder:

* Be din videospelare att regelbundet avsöka licensen för att säkerställa att inga tidsbegränsningar har gått ut. Detta kan uppnås genom att anropa `DRMManager.loadVoucher(LOCAL_ONLY).` En felkod anger att den lokalt lagrade licensen inte längre är giltig.
* När användaren klickar på **[!UICONTROL Pause]** kan du spela in den aktuella tidsstämpeln och sedan anropa `Netstream.stop()`. När användaren klickar på uppspelningsknappen kan du söka efter den inspelade platsen och sedan anropa `Netstream.play()`.

## Startdatum {#start-date}

Startdatumet anger det datum efter vilket en licens är giltig.

Exempel: Använd ett absolut datum för att utfärda innehållslicenser före tillgänglighetsdatumet för en tillgång eller för att tillämpa en&quot;embargot&quot;-period.

## Slutdatum {#end-date}

Slutdatumet anger det datum efter vilket en licens upphör att gälla.

Exempel: Använd ett absolut förfallodatum för att spegla slutet på distributionsrättigheterna.

## Relativt slutdatum {#relative-end-date}

Det relativa slutdatumet anger licensens förfallodatum, som anges i förhållande till paketeringsdatumet, inte i förhållande till det datum då licensen utfärdades.

Exempel: I en automatiserad paketeringsprocess använder du en enda Primetime DRM-princip med det här alternativet för en serie videor för att ange förfallodatumet till 30 dagar i förhållande till paketeringsdatumet.

## Licensens cachelagringstid{#license-caching-duration}

Licensens cachelagringstid anger hur länge en licens kan cachelagras på disken i klientens lokala License Store utan att licensservern behöver hämtas igen. Du kan också ange ett absolut datum och en absolut tidpunkt efter vilken en licens inte längre kan cachas.

När cachens förfallodatum har passerat är licensen inte längre giltig och klienten måste begära en ny licens från licensservern.

Exempel: Använd licensens cachelagringstid för att ange en fast tidsperiod som är giltig för en viss licens, t.ex. vid uthyrning. Du kan ange en 30-dagars uthyrning (med cache-lagring av licenser) för att ange den totala licenstiden för innehållet.

## Uppspelningsfönstret {#playback-window}

Uppspelningsfönstret anger hur länge en licens är giltig efter första gången den används för att spela upp skyddat innehåll.

Exempel: Vissa affärsmodeller tillåter en hyrperiod på 30 dagar, men när uppspelningen börjar måste uppspelningen vara slutförd på 48 timmar. I det här fallet är licensens 48-timmarsperiod uppspelningsfönstret.

**Från version 5.3 framåt**  - Uppspelningsfönstret har även stöd för alternativet att aktivera eller inaktivera Hårt stopp, vilket anger om dekrypteringssammanhanget för uppspelning ska stoppas när uppspelningsfönstret (aktiverat) upphör eller fortsätta trots att det har gått ut (inaktiverat).

>[!NOTE]
>
>Alternativet för hårddiskar fungerar inte korrekt med uppspelningsfönstret om det används tillsammans med det (uppspelningsfönstret stöds inte). Uppspelning av innehåll med uppspelningsfönstret utan säkert stopp respekterar uppspelningsfönstrets begränsning.