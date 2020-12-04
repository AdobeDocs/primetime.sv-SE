---
description: Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta redundans, signalera till manifestservern för att behandla primära strömmar och failover-strömmar som identifieras i den överordnad spellistan som frånkopplade uppsättningar (med sina egna UID).
seo-description: Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta redundans, signalera till manifestservern för att behandla primära strömmar och failover-strömmar som identifieras i den överordnad spellistan som frånkopplade uppsättningar (med sina egna UID).
seo-title: Underlätta byte av HLS-spelare till strömmar för växling vid fel/säkerhetskopiering
title: Underlätta byte av HLS-spelare till strömmar för växling vid fel/säkerhetskopiering
uuid: 2fea8a51-e4cb-4fc9-82d5-6305a1d96603
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Underlättar växling av HLS-spelare till failover-/säkerhetskopieringsströmmar {#facilitating-hls-player-switching-to-failover-backup-streams}

Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta redundans, signalera till manifestservern för att behandla primära strömmar och failover-strömmar som identifieras i den överordnad spellistan som frånkopplade uppsättningar (med sina egna UID).

För att underlätta växling till failover- eller säkerhetskopieringsströmmar på Apple HLS-enheter kan du ange parametern `ptfailover` i Bootstrap-URL:en. Om du anger den här parametern skapar manifestservern separata uppspelningssessioner (som avgör vilka annonser som sammanfogas) för varje redundansuppsättning.

## Detaljer

Hur SSAI hanterar HLS-växling till failover/säkerhetskopiering när du inkluderar `ptfailover=true` i Bootstrap-begäran:

* När en överordnad spelningslista innehåller primära och säkerhetskopierade uppsättningar:

   * Manifestservern identifierar AV-ström-URL:er för olika redundansuppsättningar med attributet `BANDWIDTH` och AV-strömmens URL:er i tolkningsordning. Den skapar separata interna uppspelningssessioner (identifieras av separata UID:n) och skapar strömmar-URL:er som pekar på manifestservrar med olika UID:n som identifierar olika uppspelningssessioner.
   * Manifestservern identifierar URL:er för I-Frame-ström för olika redundansuppsättningar med det matchande `RESOLUTION`-attributet och i-Frame-strömmens URL:er. SSAI använder UUID:n som identifierar associerade AV-strömmar för I-Frame-strömmar som pekar på SSAI.
   * För den här funktionen har manifestservern bara stöd för `EXT-X-MEDIA`-grupper utan URI-attribut i den överordnad spellistan.
   * Manifestservern identifierar ett 404-felsvar från ett CDN med ett `X-Object-Too-Old: true`-huvud och bevarar statuskoden och huvudet när svaret skickas till spelaren.

* Annonser före rullning läggs endast till i den primära uppsättningen. de är helt inaktiverade i failover-uppsättningar för att undvika felaktiga och/eller duplicerade pre-roll-annonser när spelaren växlar till failover-strömmar.

