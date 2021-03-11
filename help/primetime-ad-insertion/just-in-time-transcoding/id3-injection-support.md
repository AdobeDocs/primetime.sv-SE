---
description: Just-in-time-transcoding kan ge ID3 tidsbestämda metadata till annonskreatörer för att underlätta annonsspårning på klientsidan.
title: Använda just-in-time-omkodning för att mata in ID3 Timed Metadata-taggar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

Om Primetime Ad Insertion tar emot parametern `ptplayer=ios-mobileweb` injiceras ID3-paket i den omkodade och kreativa innan de överförs till lämpligt CDN för annonslagring.
