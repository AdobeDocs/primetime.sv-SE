---
description: Med ljudkodek 3 (AC-3, även kallat Dolby Digital®) 5.1-format, kan innehållsleverantörer komprimera storleken på flerkanalsljudfiler utan att försämra ljudkvaliteten. AC-3 är ett 5.1-format, vilket innebär att det ger fem kanaler med full bandbredd för en bättre användarupplevelse.
title: AC-3 5.1-format
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# AC-3 5.1-format {#ac-format}

Med ljudkodek 3 (AC-3, även kallat Dolby Digital®) 5.1-format, kan innehållsleverantörer komprimera storleken på flerkanalsljudfiler utan att försämra ljudkvaliteten. AC-3 är ett 5.1-format, vilket innebär att det ger fem kanaler med full bandbredd för en bättre användarupplevelse.

Mer information finns i [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

TVSDK stöder följande AC-3 5.1-funktioner:

* AC-3 surround-ljud
* Blandade/oblandade strömmar för surroundljudtyp
* Möjlighet att fråga enheten för att se om surroundljudkodeken är tillgänglig på enheten.

  Resultatet avgör vilken typ av önskad ljudkodek som är vald. Det manifest med ljudkodektyp som enheten inte kommer att använda ignoreras. Om till exempel AC-3-formatet har valts beaktas inte profiler med AAC-formatet (Advanced Audio Coding).
* Genomströmningsläge

  I genomströmningsläget ändras eller ändras inte TVSDK (beroende på enhet) Dolby-media från Decoder, i stället för att avkoda media från AC-3 5.1-formatet till ett PCM-format (multichannel pulse-code modulation). Det här mediet skickas till ljudenheten (högtalare eller mottagare) så att ljudenheten kan avkoda och spela upp Dolby-surroundströmmen.

>[!IMPORTANT]
>
>TVSDK stöder endast AC-3 5.1-funktionerna på enheten med första generationen av Amazon Fire TV.

Följande AC-3 5.1-funktioner stöds inte:

* Flerkanals AAC-ljud
* ABR över olika kodekar (AAC - AC3)

## Välj media som stöds {#section_0D7E717BE18B418D817EE017EF2375D1}

Här är det typiska arbetsflödet som inträffar när TVSDK hittar ett manifest med AC-3- och AAC-media:

1. TVSDK frågar vilken kodek som enheten kan stödja.
1. Den codec som har den högre kvaliteten är markerad.

   Här är den ordning i vilken kvalitet väljs:

   1. AC-3
   1. AAC

1. TVSDK ignorerar profiler med andra ljudkodektyper.

>[!TIP]
>
>Programmet kan inte få information om ignorerade profiler.

## Bestämma utdataläget {#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

Om en Android-enhet är ansluten till högtalarsystemet beror beslutet att spela upp innehåll i surroundläge eller stereoläge på hur enheten är konfigurerad när du bearbetar AC-3-media.

|   | **Surround-ljud** | **Stereohögtalare** |
|---|---|---|
| Enhetskonfiguration Dolby är aktiverat (eller automatiskt) | Enhetskonfiguration Dolby är aktiverat (eller automatiskt) | Stereoläge |
| Enhetskonfiguration Dolby av | Stereoläge | Stereoläge |
