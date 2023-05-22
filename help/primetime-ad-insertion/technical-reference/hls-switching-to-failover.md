---
title: Underlätta byte av HLS-spelare till strömmar för failover/säkerhetskopiering
description: Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta failover, signalera en manifestserver för att behandla primära strömmar och failover-strömmar som identifieras i den överordnad spellistan som frånkopplade uppsättningar (med sina egna UUID).
exl-id: 58c7a490-403f-41b2-bdbd-6f93e27083b0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Underlätta byte av HLS-spelare till strömmar för failover/säkerhetskopiering {#facilitating-hls-player-switching-to-failover-backup-streams}

Apple HLS-stacken stöder växling till failover-/säkerhetskopieringsströmmar om den inte kan hämta strömmar från den primära uppsättningen. För Apple HLS-enheter kan du, för att underlätta failover, signalera en manifestserver för att behandla primära strömmar och failover-strömmar som identifieras i den överordnad spellistan som frånkopplade uppsättningar (med sina egna UUID).

För att underlätta växling till failover- eller säkerhetskopieringsströmmar på Apple HLS-enheter kan du ange `ptfailover` i Bootstrap URL. Om du anger den här parametern skapar manifestservern separata uppspelningssessioner (som avgör vilka annonser som sammanfogas) för varje redundansuppsättning.

## Detaljer

Hur SSAI hanterar HLS-växling till failover/säkerhetskopiering när du inkluderar `ptfailover=true` i Bootstrap begäran:

* När en överordnad spelningslista innehåller primära och säkerhetskopierade uppsättningar:

   * Manifestservern identifierar AV-ström-URL:er för olika redundansuppsättningar med hjälp av `BANDWIDTH` och tolkningsordningen för AV-strömmens URL:er. Den skapar separata interna uppspelningssessioner (identifieras av separata UID:n) och skapar strömmar-URL:er som pekar på manifestservrar med olika UID:n som identifierar olika uppspelningssessioner.
   * Manifestservern identifierar URL:er för I-Frame-ström för olika redundansuppsättningar med hjälp av matchande `RESOLUTION` och i vilken ordning URL:er för I-Frame-ström ska tolkas. SSAI använder UUID:n som identifierar associerade AV-strömmar för I-Frame-strömmar som pekar på SSAI.
   * För den här funktionen stöds endast manifestservern `EXT-X-MEDIA` grupper utan URI-attribut i den överordnad spellistan.
   * Manifestservern identifierar ett 404-felsvar från ett CDN med ett `X-Object-Too-Old: true` och bevarar statuskoden och rubriken när svaret skickas till spelaren.

* Annonser före rullning läggs endast till i den primära uppsättningen. de är helt inaktiverade i failover-uppsättningar för att undvika felaktiga och/eller duplicerade pre-roll-annonser när spelaren växlar till failover-strömmar.
