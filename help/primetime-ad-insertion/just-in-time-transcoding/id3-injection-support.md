---
description: Just-in-time-transcoding kan ge ID3 tidsbestämda metadata till annonskreatörer för att underlätta annonsspårning på klientsidan.
seo-description: Just-in-time-transcoding kan mata in ID3-metadata i HLS-format och andra kreatörer för att underlätta annonsspårning på klientsidan.
seo-title: Använda just-in-time-omkodning för att mata in ID3 Timed Metadata-taggar
title: Använda just-in-time-omkodning för att mata in ID3 Timed Metadata-taggar
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Använda just-in-time-omvandling för att mata in ID3 Timed Metadata-taggar {#using-crs-to-inject-id-timed-metadata-tags}

CRS kan lägga in ID3-metadata i annonskreatörer för att underlätta annonsspårning på klientsidan.

Klientspelaren läser ID3-metadata för att möjliggöra bildruteexakt annonsspårning.

>[!NOTE]
>
>ID3-tidsbestämda metadatainjektionsfunktioner för Safari/iOS.

## Arbetsflöde för CRS för ID3-injektion {#workflow-for-crs-for-id3-injection}

Om Primetime Ad Insertion tar emot parametern `ptplayer=ios-mobileweb` injiceras ID3-paket i den omkodade och kreativa innan de överförs till lämpligt CDN för annonslagring.
