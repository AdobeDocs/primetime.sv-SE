---
description: För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.
seo-description: För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.
seo-title: Faktureringsstatistik
title: Faktureringsstatistik
uuid: 4a03995a-60f6-440e-9cdf-9c0b9c5f1d90
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Översikt {#billing-metrics-overview}

För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.

Varje gång spelaren genererar en direktuppspelningshändelse börjar TVSDK skicka HTTP-meddelanden regelbundet till Adobes faktureringssystem. Perioden, som kallas fakturerbar varaktighet, kan vara en annan för VOD av standardtyp, VOD av proffskvalitet (aktiverad annonsering i mellanrullar) och direktinnehåll. Standardlängden för varje innehållstyp är 30 minuter, men avtalet med Adobe avgör de faktiska värdena.

Meddelandena innehåller följande information:

* Innehållstyp (live, linear eller VOD)
* Innehålls-URL
* Om annonser är aktiverade
* Anger om annonser på mellannivå är aktiverade (endast VOD)
* Anger om strömmen skyddas av DRM
* Version och plattform för TVSDK

Adobe förkonfigurerar detta arrangemang, men du kan arbeta med din Adobe Enabled-representant för att ändra ordningen, arbeta med din Adobe Enabled-representant.

Om du vill övervaka den statistik som TVSDK skickar till Adobe hämtar du URL:en från din Adobe Enablement-representant och använder ett verktyg för nätverksregistrering, som Charles, för att se data.
