---
description: Funktionen Partial Ad Break Insertion (PABI) påminner om en TV-liknande upplevelse där användaren, om han eller hon går med i en liveström i en mellanrollsbrytning, visas på medelversionssidan i stället för en förhandsgranskningsannons eller skiffer.
title: Inläggning av delvis annonsbrytning
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Inläggning av delvis annonsbrytning {#partial-ad-break-insertion}

Funktionen Partial Ad Break Insertion (PABI) påminner om en TV-liknande upplevelse där användaren, om han eller hon går med i en liveström i en mellanrollsbrytning, visas på medelversionssidan i stället för en förhandsgranskningsannons eller skiffer.

När annonsservern returnerar pre-roll-annonser för en liveström, kommer manifestservern att mata in pre-roll-annonsbrytningen före live-point och infoga EXT-X-START-taggen med dess TIMEOFFSET-värde som pekar mot början av förrollningsannonsbrytningen. Det här standardbeteendet säkerställer att hela förrullningsannonsbrytningen spelas upp före innehållet vid direktpunkten. Om en användare ansluter till en direktuppspelning när direktpunkten är nära en annonsbrytning i mitten av rullen, visas användaren före- och radbrytningen före mittrullningsannonsbrytningen vid direktpunkten.

Funktionen PABI instruerar manifestservern att ignorera förradbrytningen och ange värdet EXT-X-START:TIMEOFFSET till början av mellanrollsannonsen som finns vid direktpunkten. Detta garanterar att användaren ser hela annonsen i mellanrullen som för närvarande spelas upp vid direktuppspelningen utan att behöva visa annonsbrytningen i pre-roll.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för liveströmmar. Manifestservern infogar en annonsbrytning före och efter VOD-spellistan som standard.

>[!NOTE]
>
>Om du vill aktivera PABI måste du ange [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) i bootstrap-URL:en.

>[!NOTE]
>
>The [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) är en HLS-standardtagg som anger en önskad startpunkt i spellistan.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Använd spårning på klientsidan eftersom klienten har större kontroll över avfyrningen av spårningsfyrar.
* Delvisa annonsbrytningar bör endast användas med spårningsläget på serversidan om spelaren stöder EXT-X-START.