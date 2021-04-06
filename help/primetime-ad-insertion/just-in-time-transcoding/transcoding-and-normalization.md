---
title: Omkodning och normalisering
description: Omkodning och normalisering
copied-description: true
exl-id: 48d9d971-4b15-4f1b-8740-c21983a3e835
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Omkodning och normalisering {#transcoding-and-normalization}

Primetime Ad Insertion kommer att försöka säkerställa en enhetlig tittarupplevelse över innehåll och annonser genom att försöka matcha:

1. Källströmskodekar och bithastigheter, men välj alltid den högsta kvaliteten/bithastigheten när du omkodar

1. Fragmentstorlekar för källström (HLS/#EXT-X-TARGETDURATION)

1. Kreativa standardformat för transkodning

1. Automatisk ljudutjämning säkerställer en konsekvent dB-nivå för alla annonskreatörer.

>[!NOTE]
>
>HLS-resurser som genereras av Primetimes Ad Insertion-just-in-tidsomkodning producerar HLS-resurser i version 3, oavsett vilken HLS-version som definieras i innehållet.
