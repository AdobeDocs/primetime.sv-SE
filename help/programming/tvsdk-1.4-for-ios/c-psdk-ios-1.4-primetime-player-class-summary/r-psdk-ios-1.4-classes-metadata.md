---
description: Dessa klasser innehåller metadata för annonsering, namnutrymmen och spårning.
title: Metadataklasser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Metadataklasser{#metadata-classes}

Dessa klasser innehåller metadata för annonsering, namnutrymmen och spårning.

| Namn | Beskrivning |
|---|---|
| [PTAdMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdMetadata.html) | En klass som innehåller egenskaper som ska konfigureras för att matcha annonser för ett visst medieobjekt. Alla nödvändiga egenskaper måste ställas in för att spelaren ska kunna matcha annonser. |
| [PTAuditudemetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) | Klass som utökas `PTAdMetadata` specifikt för Adobe Primetime annonsbeslut. Tillhandahåller egenskaper som ska konfigureras för att matcha annonser för Adobe Primetime-annonsbeslut för ett visst medieobjekt. Du måste ange alla nödvändiga egenskaper, inklusive zon-ID, medie-ID och URL för annonsserver, för att konfigurera spelaren för att kunna matcha annonser. |
| [PTMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMetadata.html) | Definierar basklassen för att konfigurera alla tillgängliga metadata för spelaren och ytterligare objekt. |
| [PTTimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTimedMetadata.html) | En klass som representerar en anpassad HLS-tagg i strömmen. |
| [PTTrackingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTrackingMetadata.html) | Definierar en basklass för alla spårnings- och analysrelaterade metadata. |
