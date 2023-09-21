---
title: Definiera tidsbaserade regler
description: Definiera tidsbaserade regler
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Definiera tidsbaserade regler {#defining-time-based-rules}

Adobe Access använder&quot;mjuk tillämpning&quot; av tidsbaserade licensbegränsningar. Om en tidsrättighet upphör vid uppspelning av en video är standardbeteendet för Adobe Access att inte begränsa uppspelningen förrän nästa gång videoflödet återskapas (genom att anropa `Netstream.stop()` och `Netstream.play()`).

Även om mjuk tvång är standardbeteendet kan du även aktivera hård tvång genom att utföra någon av följande åtgärder:

* Be din videospelare att regelbundet avsöka licensen för att säkerställa att inga tidsbegränsningar har gått ut. Detta kan uppnås genom att ringa `DRMManager.loadVoucher(LOCAL_ONLY).`En felkod anger att den lokalt lagrade licensen inte längre är giltig.
* När användaren klickar på pausknappen kan du spela in den aktuella tidsstämpeln och sedan anropa `Netstream.stop().`När användaren klickar på uppspelningsknappen kan du söka efter den inspelade platsen och sedan anropa `Netstream.play()`.

## Startdatum {#start-date}

Anger efter vilket datum en licens är giltig.

Exempel: Använd ett absolut datum för att utfärda innehållslicenser före tillgänglighetsdatumet för en tillgång eller för att tillämpa en&quot;embargot&quot;-period.

## Slutdatum {#end-date}

Anger efter vilket datum en licens upphör att gälla.

Exempel: Använd ett absolut förfallodatum för att spegla slutet på distributionsrättigheterna.

## Relativt slutdatum {#relative-end-date}

Anger licensens utgångsdatum, uttryckt i förhållande till paketeringsdatumet.

Exempel: I en automatiserad paketeringsprocess använder du en enda policy med det här alternativet för en serie videofilmer för att ange förfallodatumet till 30 dagar i förhållande till paketeringsdatumet.

## Licensens cachelagringstid {#license-caching-duration}

Anger hur länge en licens kan cachas på disken i klientens lokala License Store utan att licensservern behöver hämtas igen. Du kan också ange ett absolut datum/tid efter vilket en licens inte längre kan cachas.

När cachens förfallodatum har passerat är licensen inte längre giltig och klienten måste begära en ny licens från licensservern.

Exempel: Använd licensens cachelagringstid för att ange en fast tidsperiod som är giltig för en viss licens, t.ex. i ett uthyrningsfall. En 30-dagars uthyrning kan anges (med cache-lagring av licenser) för att ange den totala licenstiden för innehållet.

## Uppspelningsfönster {#playback-window}

Anger hur länge en licens är giltig efter första gången den används för att spela upp skyddat innehåll.

Exempel: Vissa affärsmodeller tillåter en uthyrningsperiod på 30 dagar, men när uppspelningen börjar måste den slutföras på 48 timmar. Denna 48-timmars livslängd för licensen definieras som uppspelningsfönstret.

## Krav för synkronisering {#requirements-for-synchronization}

Anger hur ofta klienten ska synkronisera sitt tillstånd med servern. Om klienten har fått en out-of-band-licens (utan att någon licensserver kontaktas) kan användningsreglerna ange att klienten måste skicka synkroniseringsmeddelanden till servern för att synkronisera klientens säkra tid och rapportera klientens tillstånd till servern.

Synkroniseringsbeteendet definieras med följande parametrar:

* Startintervall - Anger hur lång tid det tar att vänta efter den senaste lyckade synkroniseringen för att starta en annan synkroniseringsbegäran.
* Hårt stoppintervall - (valfritt). Tillåt inte uppspelning om en lyckad synkronisering inte har utförts under den angivna tiden.
* Tvinga synkroniseringssannolikhet - (valfritt). Sannolikhet med vilken klienten ska skicka ett synkroniseringsmeddelande före nästa startintervall.

>[!NOTE]
>
>Den här användningsregeln stöds av Adobe Access-klienter version 3.0 och senare. Beteendet för äldre klienter beror på den lägsta klientversion som stöds av licensservern. Se, [Minsta klientversion](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).
