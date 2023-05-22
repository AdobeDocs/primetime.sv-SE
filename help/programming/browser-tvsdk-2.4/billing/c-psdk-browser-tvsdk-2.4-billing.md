---
description: För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.
title: Faktureringsstatistik
exl-id: f4200573-571f-4ed3-be8c-08b72d4f9e0e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Översikt {#billing-metrics-overview}

För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.

Varje gång spelaren genererar en starthändelse för direktuppspelning börjar webbläsaren TVSDK att skicka HTTP-meddelanden regelbundet till Adobe. Perioden, som kallas fakturerbar varaktighet, kan vara en annan för VOD av standardtyp, VOD av proffskvalitet (aktiverad annonsering i mellanrullar) och direktinnehåll. Standardlängden för varje innehållstyp är 30 minuter, men ditt kontrakt med Adobe avgör de faktiska värdena.

Meddelandena innehåller följande information:

* Innehållstyp (live, linear eller VOD)
* Innehålls-URL
* Om annonser är aktiverade
* Anger om annonser på mellannivå är aktiverade (endast VOD)
* Anger om strömmen skyddas av DRM
* Version och plattform för webbläsaren TVSDK

Adobe förkonfigurerar det här arrangemanget, men om du vill ändra ordningen ska du arbeta med din representant för Adobe Enablement.

Om du vill övervaka den statistik som webbläsaren TVSDK skickar till Adobe hämtar du URL:en från din Adobe Enablement-representant och använder ett verktyg för nätverksregistrering, till exempel Charles, för att se data.
