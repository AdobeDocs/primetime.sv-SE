---
title: Omkodning och normalisering
description: null
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '89'
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