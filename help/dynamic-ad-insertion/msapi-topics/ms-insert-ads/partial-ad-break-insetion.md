---
description: Funktionen Partial Ad Break Insertion (PABI) påminner om en TV-liknande upplevelse där användaren, om han eller hon går med i en liveström i en mellanrollsbrytning, visas på medelversionssidan i stället för en förhandsgranskningsannons eller skiffer.
seo-description: Funktionen Partial Ad Break Insertion (PABI) påminner om en TV-liknande upplevelse där användaren, om han eller hon går med i en liveström i en mellanrollsbrytning, visas på medelversionssidan i stället för en förhandsgranskningsannons eller skiffer.
seo-title: Inläggning av delvis annonsbrytning
title: Inläggning av delvis annonsbrytning
uuid: a0c1ae34-0f8d-4401-97fe-45a2ea40d08d
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Inläggning av partiell annonsbrytning {#partial-ad-break-insertion}

Funktionen Partial Ad Break Insertion (PABI) påminner om en TV-liknande upplevelse där användaren, om han eller hon går med i en liveström i en mellanrollsbrytning, visas på medelversionssidan i stället för en förhandsgranskningsannons eller skiffer.

När annonsservern returnerar pre-roll-annonser för en liveström, kommer manifestservern att mata in pre-roll-annonsbrytningen före live-point och infoga EXT-X-START-taggen med dess TIMEOFFSET-värde som pekar mot början av förrollningsannonsbrytningen. Det här standardbeteendet säkerställer att hela förrullningsannonsbrytningen spelas upp före innehållet vid direktpunkten. Om en användare ansluter till en direktuppspelning när direktpunkten är nära en annonsbrytning i mitten av rullen, kommer användaren att visas före- och radbrytningen före den aktiva punkten.

Funktionen PABI instruerar manifestservern att ignorera förradbrytningen och ange värdet EXT-X-START:TIMEOFFSET till början av mellanrollsannonsen som finns vid direktpunkten. Detta garanterar att användaren ser hela annonsen i mellanrullen som för närvarande spelas upp vid direktuppspelningen utan att behöva visa annonsbrytningen i pre-roll.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för liveströmmar. Manifestservern infogar en annonsbrytning före och efter VOD-spellistan som standard.

>[!NOTE]
>
>Om du vill aktivera PABI måste du ange [query_params](../../msapi-topics/ms-getting-started/ms-api-query-params.md) i bootstrap-URL:en.

>[!NOTE]
>
>[EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) är en HLS-standardtagg som anger en önskad startpunkt i spellistan.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Använd spårning på klientsidan eftersom klienten har större kontroll över avfyrningen av spårningsfyrar.
* Delvisa annonsbrytningar bör endast användas med spårningsläget på serversidan om spelaren stöder EXT-X-START.