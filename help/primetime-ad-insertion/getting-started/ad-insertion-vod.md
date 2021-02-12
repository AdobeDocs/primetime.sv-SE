---
title: Använd Ad Insertion för VOD
description: Använda Ad Insertion för VOD
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Använd Ad Insertion för VOD {#ad-insertion-vod}

Primetime Ad Insertion stöder annonsinfogning i flera VOD-resurser med hjälp av VAST 3.0+ eller VMAP 1.0+.

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (annonskartor) {#server-mapped-ads}

Primetime Ad Insertion stöder VOD-infogning med annonser som infogats före uppspelningens början med hjälp av annonstidslinjeinformation som definierats i ett VMAP-format.  VMAP-specifik annonsspårning som breakStart/breakEnd-fyrar levereras med [annonsspårning](set-up-ad-tracking.md).

## Full Event Replay (VOD med Ad Decisioning Cues) {#full-event-replay}

Primetime Ad Insertion stöder också specialiserade VOD-resurser som innehåller tips i själva innehållsströmmen, som exempelvis i uppspelning av tidigare inspelade livehändelser. Mer information om vilka typer av annonsinstruktioner (eller cue-format) som stöds finns i [Använda Ad Insertion i Live/Linear](ad-insertion-live-linear-stream.md).

Vi stöder både enstaka annonsförfrågningar och parallella olika annonsscenarier för VOD-resurser som innehåller mer än en annonsbrytning. Mer information finns i `ptmulticall`-parametern i [Parameterbeskrivning](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md). Både VAST- och VMAP-format stöds för cues i strömmen.
