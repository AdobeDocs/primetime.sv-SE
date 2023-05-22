---
title: Externt CEK-arbetsflöde för AXS DRM
description: Det här arbetsflödet skiljer sig från de flesta befintliga DRM-system eftersom det inte kräver att något centralt arkiv eller CMS (Content Key Management System) används
exl-id: f084aa57-8bef-40a0-b52d-4d23dfdf36c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Externt CEK-arbetsflöde för AXS DRM{#aaxs-drm-external-cek-workflow}

Det här arbetsflödet skiljer sig från de flesta befintliga DRM-system eftersom det inte kräver att något centralt arkiv eller CMS (Content Key Management System) används. För kunder som vill att AAXS ska fungera med sina befintliga CKMS-system har AXS dock en funktion som kallas &quot;External CEK&quot;, där CEK levereras externt vid paketerings- och licensutfärdandetid.

![](assets/ECEK_Workflow.PNG)

1. (Paket) AAXS Java SDK levereras med ett CEK och ett CEK-ID.
1. (Paket) CEK används för att kryptera innehåll.
1. (Paket) CEK-ID infogas i innehållets DRM-metadata.
1. Enheten försöker spela upp innehåll genom att begära en licens från AXS-servern.
1. (Licensiering) AAXS-servern extraherar CEK-ID:t från innehållets metadata.
1. AAXS-servern hämtar CEK från CKMS.
1. (Licensiering) AAXS-servern utfärdar en licens som innehåller CEK till enheten.
