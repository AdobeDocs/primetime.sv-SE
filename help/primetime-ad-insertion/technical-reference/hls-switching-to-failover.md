---
title: Underlätta byte av HLS-spelare till strömmar för failover/säkerhetskopiering
description: Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta failover, signalera till manifestservern för att behandla primära strömmar och failover-strömmar som identifieras i huvudspelningslistan som frånkopplade uppsättningar (med sina egna UUID).
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Underlätta byte av HLS-spelare till strömmar för failover/säkerhetskopiering {#facilitating-hls-player-switching-to-failover-backup-streams}

Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta failover, signalera till manifestservern för att behandla primära strömmar och failover-strömmar som identifieras i huvudspelningslistan som frånkopplade uppsättningar (med sina egna UUID).

För att underlätta växling till failover- eller säkerhetskopieringsströmmar på Apple HLS-enheter kan du ange `ptfailover` i Bootstrap URL. Om du anger den här parametern skapar manifestservern separata uppspelningssessioner (som avgör vilka annonser som sammanfogas) för varje redundansuppsättning.

## Information

Hur SSAI hanterar HLS-växling till failover/säkerhetskopiering när du inkluderar `ptfailover=true` i Bootstrap begäran:

* När en huvudspelningslista innehåller primära och säkerhetskopierade uppsättningar:

   * Manifestservern identifierar AV-ström-URL:er för olika redundansuppsättningar med `BANDWIDTH` och tolkningsordningen för AV-strömmens URL:er. Den skapar separata interna uppspelningssessioner (identifieras av separata UID:n) och skapar strömmar-URL:er som pekar på manifestservrar med olika UID:n som identifierar olika uppspelningssessioner.
   * Manifestservern identifierar URL:er för I-Frame-ström för olika redundansuppsättningar med hjälp av matchande `RESOLUTION` och i vilken ordning URL:er för I-Frame-ström ska tolkas. SSAI använder UUID:n som identifierar associerade AV-strömmar för I-Frame-strömmar som pekar på SSAI.
   * För den här funktionen stöds endast manifestservern `EXT-X-MEDIA` grupper utan URI-attribut i huvudspelningslistan.
   * Manifestservern identifierar ett 404-felsvar från ett CDN med ett `X-Object-Too-Old: true` och bevarar statuskoden och rubriken när svaret skickas till spelaren.

* Annonser före rollning läggs bara till i den primära uppsättningen. De är helt inaktiverade i failover-uppsättningar för att undvika felaktiga och/eller duplicerade annonser före rollroll när spelaren växlar till failover-strömmar.
