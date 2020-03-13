---
description: Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta redundans, signalera till manifestservern för att behandla primära strömmar och failover-strömmar som identifieras i huvudspelningslistan som frånkopplade uppsättningar (med sina egna UUID).
seo-description: Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta redundans, signalera till manifestservern för att behandla primära strömmar och failover-strömmar som identifieras i huvudspelningslistan som frånkopplade uppsättningar (med sina egna UUID).
seo-title: Underlätta byte av HLS-spelare till strömmar för växling vid fel/säkerhetskopiering
title: Underlätta byte av HLS-spelare till strömmar för växling vid fel/säkerhetskopiering
uuid: 2fea8a51-e4cb-4fc9-82d5-6305a1d96603
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff

---


# Underlätta byte av HLS-spelare till strömmar för växling vid fel/säkerhetskopiering {#facilitating-hls-player-switching-to-failover-backup-streams}

Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta redundans, signalera till manifestservern för att behandla primära strömmar och failover-strömmar som identifieras i huvudspelningslistan som frånkopplade uppsättningar (med sina egna UUID).

För att underlätta växling till failover- eller säkerhetskopieringsströmmar på Apple HLS-enheter kan du ange parametern `ptfailover` i Bootstrap-URL:en. Om du anger den här parametern skapar manifestservern separata uppspelningssessioner (som avgör vilka annonser som sammanfogas) för varje redundansuppsättning.

## Detaljer

Hur SSAI hanterar HLS-växling till failover/säkerhetskopiering när du tar med `ptfailover=true` i Bootstrap-begäran:

* När en huvudspelningslista innehåller primära och säkerhetskopierade uppsättningar:

   * Manifestservern identifierar AV-ströms-URL:er för olika redundansuppsättningar med hjälp av attributet och parsningsordningen för AV-strömmens URL:er. `BANDWIDTH` Den skapar separata interna uppspelningssessioner (identifieras av separata UID:n) och skapar strömmar-URL:er som pekar på manifestservrar med olika UID:n som identifierar olika uppspelningssessioner.
   * Manifestservern identifierar URL:er för I-Frame-ström för olika redundansuppsättningar med hjälp av det matchande `RESOLUTION` -attributet och i-Frame-strömmens URL:er i parsningsordning. SSAI använder UUID:n som identifierar associerade AV-strömmar för I-Frame-strömmar som pekar på SSAI.
   * För den här funktionen stöder manifestservern bara `EXT-X-MEDIA` grupper utan URI-attribut i huvudspelningslistan.
   * Manifestservern identifierar ett 404-felsvar från ett CDN med ett `X-Object-Too-Old: true` huvud och bevarar statuskoden och huvudet när svaret skickas till spelaren.

* Annonser före rullning läggs endast till i den primära uppsättningen. de är helt inaktiverade i failover-uppsättningar för att undvika felaktiga och/eller duplicerade pre-roll-annonser när spelaren växlar till failover-strömmar.

