---
description: CRS kan mata in ID3-metadata i HLS-format och andra kreatörer för att underlätta annonsspårning på klientsidan.
seo-description: CRS kan mata in ID3-metadata i HLS-format och andra kreatörer för att underlätta annonsspårning på klientsidan.
seo-title: Använda CRS för att mata in ID3 Timed Metadata-taggar
title: Använda CRS för att mata in ID3 Timed Metadata-taggar
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: c2216a5089d23ca1fcbb77c87b4a01a6fa1807ff
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Använda CRS för att mata in ID3 Timed Metadata-taggar {#using-crs-to-inject-id-timed-metadata-tags}

CRS kan mata in ID3-metadata i HLS-format och andra kreatörer för att underlätta annonsspårning på klientsidan.

Klientspelaren läser ID3-metadata för att möjliggöra bildruteexakt annonsspårning.

>[!NOTE]
>
>Injektion av metadata i ID3 fungerar endast i Safari på iOS.

## Arbetsflöde för CRS för ID3-injektion {#workflow-for-crs-for-id3-injection}

Arbetsflödet för ID3-injektion är detsamma som i [Detaljerade arbetsflöden för JIT-ompaketering.](../creative-repackaging-service/jit-repackage.md) Om manifestservern tar emot  `ptplayer=ios-mobileweb` parametern instrueras CRS att mata in ID3-paket i den omkodade och kreativa innan den överförs till CDN-servern.

>[!NOTE]
>
>I en multi-CDN-konfiguration använder manifestservern parametern `ptcdn` i bootstrap-URL:en för att identifiera CDN-servern för att överföra annonsens kreativitet.