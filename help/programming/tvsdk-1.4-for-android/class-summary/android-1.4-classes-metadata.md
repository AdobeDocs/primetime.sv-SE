---
description: Dessa klasser innehåller metadata för annonsering, namnutrymmen och spårning.
seo-description: Dessa klasser innehåller metadata för annonsering, namnutrymmen och spårning.
seo-title: Metadataklasser
title: Metadataklasser
uuid: 6d5099c8-d562-4635-9ef0-068cc6fb9f82
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Metadataklasser{#metadata-classes}

Dessa klasser innehåller metadata för annonsering, namnutrymmen och spårning.

Paket: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Namn | Beskrivning |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | En klass som innehåller egenskaper som ska konfigureras för att matcha annonser för ett visst medieobjekt. Alla nödvändiga egenskaper måste ställas in för att spelaren ska kunna matcha annonser. |
| AuditudeMetadata | Föråldrat. Använd AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | En klass som utökar Java `AdvertisingMetadata` specifikt för fras. Tillhandahåller egenskaper som ska konfigureras för att matcha Phrase-annonser för ett visst medieobjekt. Du måste ange alla nödvändiga egenskaper, inklusive zon-ID, medie-ID och URL för annonsserver, för att konfigurera spelaren för att kunna matcha annonser. |
| [Metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Definierar det generiska gränssnittet för att konfigurera alla tillgängliga metadata för spelaren och ytterligare objekt. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Allmän datastrukturliknande klass för lagring av godtyckliga nyckelvärdepar. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | En klass för Raw-representationen av tidsbestämda metadata som infogats i en medieström. |