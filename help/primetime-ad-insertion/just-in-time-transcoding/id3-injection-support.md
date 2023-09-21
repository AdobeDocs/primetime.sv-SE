---
description: Just-in-time-transcoding kan ge ID3 tidsbestämda metadata till annonskreatörer för att underlätta annonsspårning på klientsidan.
title: Använda just-in-time-omvandling för att mata in ID3 Timed Metadata-taggar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Använda just-in-time-omvandling för att mata in ID3 Timed Metadata-taggar {#using-crs-to-inject-id-timed-metadata-tags}

CRS kan lägga in ID3-metadata i annonskreatörer för att underlätta annonsspårning på klientsidan.

Klientspelaren läser ID3-metadata för att möjliggöra bildruteexakt annonsspårning.

>[!NOTE]
>
>ID3-tidsbestämda metadatainjektionsfunktioner för Safari/iOS.

## Arbetsflöde för CRS för ID3-injektion {#workflow-for-crs-for-id3-injection}

Om Primetime Ad Insertion får `ptplayer=ios-mobileweb` kommer ID3-paket att injiceras i den omkodade och kreativa innan de överförs till lämpligt CDN för annonslagring.
