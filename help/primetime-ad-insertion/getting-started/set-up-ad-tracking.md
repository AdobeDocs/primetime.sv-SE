---
title: Ställ in annonsspårning
description: Konfigurera annonsspårning
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Konfigurera annonsspårning {#ser-up-ad-tracking}

De flesta annonsörer behöver information om när, hur länge och hur bra deras annonser har visats. Primetime Ad Insertion har stöd för annonsspårning på klientsidan, serversidan och hybridsidan, vilket ger flexibilitet vid insamlandet av denna information.

## Annonsuppföljning på klientsidan med VMAP/JSON {#client-side-ad-tracking-vmap-json}

Vid annonsspårning på klientsidan skickar servern en JSON-, VMAP- eller in-manifest-struktur till klienten som anger spårningshändelser och URL:er tillsammans med den sydda spellistan.

Om du vill aktivera annonsspårning på klientsidan anger du följande parametrar i [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>Om du anger `pttrackingmode=simple` returneras ett JSON-svar i stället för ett HLS- eller DASH-dokument om den inledande start-API-begäran anges.

<!-- **Daniel to check. The specified file in this statement does not exist.** 
More information about `pttrackingmode`, `pttrackingversion` formats, can be found in [API Reference: Manifest server query parameters](manifest-server-query-parameters.md). -->

<!--Show examples of how to request a sidecar] -->

## Annonsspårning på serversidan {#server-side-ad-tracking}

Med den här metoden beräknas annonsspårningsdata helt och hållet på serversidan. Detta är användbart när det inte går att uppdatera klientprogrammet. Annonsspårning på serversidan kanske inte matchar uppspelningsaktiviteten på klientsidan. Servern ser till exempel en annons som spelas upp när segmenten har levererats, även om slutanvändaren inte ser hela annonsen.

Om du vill aktivera annonsspårning på serversidan anger du följande parameter i [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

`pttrackingmode=sstm`

Se `pttrackingmode` avsnitt i [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).

Alla reklamspårningsfyrar skickas med följande rubriker för HTTP-begäran:

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

Dessa värden innehåller klient-/spelarens användar-agent och klientens IP-adress.

## Hybrid-annonsspårning {#hybrid-ad-tracking}

Det här arbetssättet fungerar som spårning på serversidan, men klientprogrammet begär även sidovagnar från Primetime Ad Insertion för detaljerad spårningsinformation. Hybrid-annonsspårning kan leverera icke-linjära annonser som övertäckningar och följesedlar till klientapplikationen, samtidigt som Primetime Ad Insertion fortfarande förlitar sig på att skicka enskilda URL:er för annonsspårning.
Mer information om hur du aktiverar hybridannonsspårning finns i parametern `pttrackingmode` i [Bootstrap-API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
