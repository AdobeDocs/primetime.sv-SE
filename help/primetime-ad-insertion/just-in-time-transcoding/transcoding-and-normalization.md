---
title: Omkodning och normalisering
description: Omkodning och normalisering
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Omkodning och normalisering {#transcoding-and-normalization}

Primetime Ad Insertion kommer att försöka säkerställa en enhetlig tittarupplevelse över innehåll och annonser genom att försöka matcha:

1. Källströmskodekar och bithastigheter, men välj alltid den högsta kvaliteten/bithastigheten när du kodar om

1. Källströmsfragmentstorlekar (HLS/#EXT-X-TARGETDURATION)

1. Kreativa standardformat för transkodning

1. Automatisk ljudutjämning säkerställer en konsekvent dB-nivå för alla annonskreatörer.

>[!NOTE]
>
>HLS-resurser som genereras av Primetimes Ad Insertion-just-in-tidsomkodning producerar HLS-resurser i version 3, oavsett vilken HLS-version som definieras i innehållet.
