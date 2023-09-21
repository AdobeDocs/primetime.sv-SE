---
description: Dessa klasser innehåller metadata för annonsering, namnutrymmen och spårning.
title: Metadataklasser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Metadataklasser{#metadata-classes}

Dessa klasser innehåller metadata för annonsering, namnutrymmen och spårning.

Paket: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Namn | Beskrivning |
|---|---|
| [Reklammetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | En klass som innehåller egenskaper som ska konfigureras för att matcha annonser för ett visst medieobjekt. Alla nödvändiga egenskaper måste ställas in för att spelaren ska kunna matcha annonser. |
| Auditudemetadata | Föråldrat. Använd AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | En klass som utökar Java `AdvertisingMetadata` specifikt för fras. Tillhandahåller egenskaper som ska konfigureras för att matcha Phrase-annonser för ett visst medieobjekt. Du måste ange alla nödvändiga egenskaper, inklusive zon-ID, medie-ID och URL för annonsserver, för att konfigurera spelaren för att kunna matcha annonser. |
| [Metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Definierar det generiska gränssnittet för att konfigurera alla tillgängliga metadata för spelaren och ytterligare objekt. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Allmän datastrukturliknande klass för lagring av godtyckliga nyckelvärdepar. |
| [TimedMetata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | En klass för Raw-representationen av tidsbestämda metadata som infogats i en medieström. |
