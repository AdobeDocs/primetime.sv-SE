---
description: Just-in-time-transcoding kan ge ID3 tidsbestämda metadata till annonskreatörer för att underlätta annonsspårning på klientsidan.
title: Använda just-in-time-omkodning för att mata in ID3 Timed Metadata-taggar
exl-id: 6171223a-71f9-45a2-a3f5-7ede4a9b101a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Använda Just-in-Time-omkodning för att mata in ID3 Timed Metadata-taggar {#using-crs-to-inject-id-timed-metadata-tags}

CRS kan lägga in ID3-metadata i annonskreatörer för att underlätta annonsspårning på klientsidan.

Klientspelaren läser ID3-metadata för att möjliggöra bildruteexakt annonsspårning.

>[!NOTE]
>
>ID3-tidsbestämda metadatainjektionsfunktioner för Safari/iOS.

## Arbetsflöde för CRS för ID3-injektion {#workflow-for-crs-for-id3-injection}

Om Primetime Ad Insertion får `ptplayer=ios-mobileweb` -parametern kommer ID3-paket att injiceras i den omkodade och kreativa innan de överförs till lämpligt CDN för annonslagring.
