---
description: För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.
title: Faktureringsstatistik
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Faktureringsstatistik {#billing-metrics}

För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.

Varje gång spelaren genererar en direktuppspelningshändelse börjar TVSDK skicka HTTP-meddelanden regelbundet till Adobe faktureringssystem. Perioden, som kallas fakturerbar varaktighet, kan vara en annan för VOD av standardtyp, VOD av proffskvalitet (aktiverad annonsering i mellanrullar) och direktinnehåll. Standardlängden för varje innehållstyp är 30 minuter, men ditt kontrakt med Adobe avgör de faktiska värdena.

Meddelandena innehåller följande information:

* Innehållstyp (live, linear eller VOD)
* Innehålls-URL
* Om annonser är aktiverade
* Anger om annonser på mellannivå är aktiverade (endast VOD)
* Anger om strömmen skyddas av DRM
* TVSDK-versionen och -plattformen

Adobe förkonfigurerar det här arrangemanget, men du kan arbeta med din representant för Adobe Enablement för att ändra ordningen, arbeta med din representant för Adobe Enablement.

Om du vill övervaka den statistik som TVSDK skickar till Adobe hämtar du URL-adressen från din representant för Adobe Enablement och använder ett verktyg för nätverksregistrering, som Charles, för att se data.
