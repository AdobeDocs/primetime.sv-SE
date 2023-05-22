---
title: Använd Ad Insertion för VOD
description: Använda Ad Insertion för VOD
exl-id: c998938e-f8a6-4ad3-97f6-ca4ad5055f15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Använd Ad Insertion för VOD {#ad-insertion-vod}

Primetime Ad Insertion stöder annonsinfogning i flera VOD-resurser med hjälp av VAST 3.0+ eller VMAP 1.0+.

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (annonskartor) {#server-mapped-ads}

Primetime Ad Insertion stöder VOD-infogning med annonser som infogats före uppspelningens början med hjälp av annonstidslinjeinformation som definierats i ett VMAP-format.  VMAP-specifik annonsspårning som breakStart/breakEnd-fyrar levereras med [Annonsuppföljning](set-up-ad-tracking.md).

## Full Event Replay (VOD med Ad Decisioning Cues) {#full-event-replay}

Primetime Ad Insertion stöder också specialiserade VOD-resurser som innehåller tips i själva innehållsströmmen, som exempelvis i uppspelning av tidigare inspelade livehändelser. Mer information om vilka typer av cues för annonsbeslut (eller cue-format) som stöds finns i [Använda Ad Insertion i Live/Linear](ad-insertion-live-linear-stream.md).

Vi stöder både enstaka annonsförfrågningar och parallella olika annonsscenarier för VOD-resurser som innehåller mer än en annonsbrytning. Mer information finns i `ptmulticall` parameter in [Parameterbeskrivning](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md). Både VAST- och VMAP-format stöds för cues i strömmen.
