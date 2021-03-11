---
description: Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade medier.
title: AC-3 5.1-format
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# AC-3 5.1-format{#ac-format}

Direktuppspelning över Internet kräver en konstant och stabil anslutning för att spela upp en ström från en fjärrserver. Skillnaden mellan en tittares internetanslutning eller direktuppspelning innebär dock att fjärruppspelningen kanske inte har samma kvalitet som lokalt uppspelade medier.

Primetime kan inte skydda mot fel som ett avbrott i en Internet-leverantör eller en kabelbortkoppling. Primetime-strömning ger dock failover-skydd för att skydda uppspelningen från vissa fjärrserverfel eller driftfel, vilket ger en bättre upplevelse för tittarna. TVSDK implementerar redundansskydd för att minimera uppspelningsavbrott och få en sömlös uppspelning trots överföringsproblem. Videospelaren växlar automatiskt till en uppsättning säkerhetskopieringsmedia när hela återgivningar eller fragment inte är tillgängliga.

Med ljudkodek 3 (AC-3, även kallat Dolby Digital®) 5.1-format, kan innehållsleverantörer komprimera storleken på flerkanalsljudfiler utan att försämra ljudkvaliteten. AC-3 är ett 5.1-format, vilket innebär att det ger fem kanaler med full bandbredd för en bättre användarupplevelse.

Mer information finns i [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

>[!IMPORTANT]
>
>TVSDK version 1.4 har endast stöd för AC-3 5.1-formatet på Amazon FireTV.

TVSDK stöder följande AC-3 5.1-funktioner:

* AC-3 surround-ljud
* Blandade/oblandade strömmar för surroundljudtyp
* Möjlighet att fråga enheten för att se om surroundljudkodeken är tillgänglig på enheten.

   Resultatet avgör vilken typ av önskad ljudkodek som är vald. Det manifest med ljudkodektyp som enheten inte kommer att använda ignoreras. Om till exempel AC-3-formatet har valts beaktas inte profiler med AAC-formatet (Advanced Audio Coding).
* Genomströmningsläge

   I genomströmningsläget ändras eller ändras inte TVSDK (beroende på enhet) Dolby-media från Decoder, i stället för att avkoda media från AC-3 5.1-formatet till ett PCM-format (multichannel pulse-code modulation). Det här mediet skickas till ljudenheten (högtalare eller mottagare) så att ljudenheten kan avkoda och spela upp Dolby-surroundströmmen.

TVSDK stöder endast AC-3 5.1-funktionerna på enheten med första generationen av Amazon Fire TV.

Följande AC-3 5.1-funktioner stöds inte:

* Flerkanals AAC-ljud
* ABR över olika kodekar (AAC - AC3)

## Välja media som stöds {#section_E1DFA1F472EA4BDE846C71A3343E275A}

Här är det typiska arbetsflödet som inträffar när TVSDK hittar ett manifest med AC-3- och AAC-media:

1. TVSDK frågar vilken kodek som enheten kan stödja.
1. Den codec som har den högre kvaliteten markeras.

   Kvalitetsordningen är AC-3 > AAC.
1. TVSDK ignorerar profiler med andra ljudkodektyper.

>[!TIP]
>
>Programmet kan inte få information om ignorerade profiler.

## Bestämma utdataläget {#section_64145D9824594C36AADBF0482C528767}

Om en Android-enhet är ansluten till högtalarsystemet beror beslutet att spela upp innehåll i surroundläge eller stereoläge på hur enheten är konfigurerad när du bearbetar AC-3-media.

|  | Surround-ljud | Stereohögtalare |
|---|---|---|
| Enhetskonfiguration Dolby är aktiverat (eller automatiskt) | Enhetskonfiguration Dolby är aktiverat (eller automatiskt) | Stereoläge |
| Enhetskonfiguration Dolby av | Stereoläge | Stereoläge |

