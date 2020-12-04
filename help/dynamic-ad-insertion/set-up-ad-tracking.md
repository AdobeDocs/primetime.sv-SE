---
title: Ställ in annonsspårning
description: Konfigurera annonsspårning
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Konfigurera annonsspårning {#ser-up-ad-tracking}

De flesta annonsörer behöver information om när, hur länge och hur bra deras annonser har visats. Primetime Ad Insertion har stöd för annonsspårning på klientsidan, serversidan och hybridsidan, vilket ger flexibilitet vid insamlandet av denna information.

## Annonsuppföljning på klientsidan med VMAP/JSON {#client-side-ad-tracking-vmap-json}

Vid annonsspårning på klientsidan skickar servern en JSON-, VMAP- eller in-manifest-struktur till klienten som anger spårningshändelser och URL:er tillsammans med den sydda spellistan.

Om du vill aktivera annonsspårning på klientsidan anger du följande parametrar i [Bootstrap API](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md).

* `pttrackingmode=simple`

* `pttrackingversion={format version (vmap,v1,v2,v3)}`

>[!NOTE]
>
>Om du anger `pttrackingmode=simple` returneras ett JSON-svar i stället för ett HLS- eller DASH-dokument om den inledande start-API-begäran anges.

Mer information om `pttrackingmode`, `pttrackingversion`-format finns i [API-referens: Frågeparametrar för manifestserver](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md).

## Annonsspårning på serversidan {#server-side-ad-tracking}

Med den här metoden beräknas annonsspårningsdata helt och hållet på serversidan. Detta är användbart när det inte går att uppdatera klientprogrammet. Annonsspårning på serversidan kanske inte matchar uppspelningsaktiviteten på klientsidan. Servern ser till exempel en annons som spelas upp när segmenten har levererats, även om slutanvändaren inte ser hela annonsen.

Om du vill aktivera annonsspårning på serversidan anger du följande parameter i [Bootstrap API](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md).

`pttrackingmode=sstm`

Se `pttrackingmode` avsnitt i [Bootstrap API](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md).

Alla reklamspårningsfyrar skickas med följande rubriker för HTTP-begäran:

* `X-Forwarded-For`
* `User-Agent`
* `X-Device-User-Agent`

Dessa värden innehåller klient-/spelarens användar-agent och klientens IP-adress.

## Hybrid-annonsspårning {#hybrid-ad-tracking}

Det här arbetssättet fungerar som spårning på serversidan, men klientprogrammet begär även sidovagnar från Primetime Ad Insertion för detaljerad spårningsinformation. Hybrid-annonsspårning kan leverera icke-linjära annonser som övertäckningar och följesedlar till klientapplikationen, samtidigt som Primetime Ad Insertion fortfarande förlitar sig på att skicka enskilda URL:er för annonsspårning.
Mer information om hur du aktiverar hybridannonsspårning finns i parametern `pttrackingmode` i [Bootstrap-API](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md).
