---
description: Använd valfria frågeparametrar för paketläge, paketversion och paketposition för att hämta URL:er dit annonsspårningsinformation om den aktuella videon ska skickas. Svaren varierar beroende på spårningsversionen och om videoströmmen är live eller on demand (VOD).
title: API för spelare som ska interagera med manifestservern
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# API för spelare som ska interagera med manifestservern {#api-for-players-to-interact-with-the-manifest-server}

Använd de valfria frågeparametrarna `pttrackingmode`, `pttrackingversion` och `pttrackingposition` för att hämta URL:er dit annonsspårningsinformation om den aktuella videon ska skickas. Svaren varierar beroende på spårningsversionen och om videoströmmen är live eller on demand (VOD).

## Frågeparametrar {#query-parameters}

**pttrackingmode**

Exempel: `pttrackingmode=simple`
Om du anger enkel anger det för manifestservern att du vill ha spårningsinformation.
Ange det på en begäran att hämta M3U8 innan du begär spårningsinformation. Om du inte anger det returnerar manifestservern spårningsinformation i #EXT-X-MARKER-taggarna.
Om du anger ett annat giltigt värde än enkelt anropas spårning på serversidan.

**pttrackingversion**

Exempel: `pttrackingversion=v2`
Den här parametern anger vilket format som ska användas för att returnera spårningsinformation (se [Filformat](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Ange det på en begäran att hämta M3U8 innan du begär spårningsinformation. När du inte anger det, eller anger ett ogiltigt värde, använder manifestservern v1.

**pttrackingposition**

Exempel: `pttrackingposition`
Den här parametern anger för manifestservern att returnera spårningsinformation för videon som ett JSON- eller VMAP-objekt i M3U8-filen. Manifestservern ignorerar det angivna värdet och skickar all spårningsinformation som den har för sessionen. Om inget värde skickas returnerar manifestservern den begärda M3U8-filen.
