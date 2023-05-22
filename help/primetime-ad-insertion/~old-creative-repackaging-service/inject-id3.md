---
description: CRS kan mata in ID3-metadata i HLS-format och andra kreatörer för att underlätta annonsspårning på klientsidan.
title: Använda CRS för att mata in ID3 Timed Metadata-taggar
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Använda CRS för att mata in ID3 Timed Metadata-taggar {#using-crs-to-inject-id-timed-metadata-tags}

CRS kan mata in ID3-metadata i HLS-format och andra kreatörer för att underlätta annonsspårning på klientsidan.

Klientspelaren läser ID3-metadata för att möjliggöra bildruteexakt annonsspårning.

>[!NOTE]
>
>Injektion av metadata i ID3 fungerar endast i Safari på iOS.

## Arbetsflöde för CRS för ID3-injektion {#workflow-for-crs-for-id3-injection}

Arbetsflödet för ID3-injektion är detsamma som i [Detaljerade arbetsflöden för JIT-ompaketering.](../~old-creative-repackaging-service/jit-repackage.md) Om manifestservern tar emot `ptplayer=ios-mobileweb` anger den att CRS ska mata in ID3-paket i den omkodade och kreativa innan de överförs till CDN-servern.

>[!NOTE]
>
>I en multi-CDN-konfiguration använder manifestservern `ptcdn` -parametern i bootstrap-URL för att identifiera CDN-servern som ska överföra annonsens kreativitet.