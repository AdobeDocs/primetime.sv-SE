---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
title: Videoanalys
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Videoanalys{#video-analytics}

Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.

Videospårning i TVSDK använder **Adobe Analytics Video Essentials** som tillhandahåller interaktionsstatistik för video, som videovisningar, kompletta videofilmer, annonsvisningar, tidsåtgång för video och så vidare. Mer information om den här tjänsten får du av Adobe.

Följande procedur sammanfattar stegen som krävs för att aktivera videospårning i spelaren:

1. Initiera och/eller konfigurera följande videospårningskomponenter:

   * **AppMeasurementen bibliotek** - Innehåller den grundläggande logiken för datainsamling på låg nivå. Det är här som videons pulsslagdata samlas in och skickas över nätverket.
   * **Bibliotek för videohjärtslag** - Innehåller kärnlogik för datainsamling med pulsslag. Biblioteket för videohjärtslag har åtkomst till en delmängd av `AppMeasurement` biblioteks-API:er.

     >[!TIP]
     >
     >Din app interagerar inte direkt med videons hjärtslagskod. I stället använder appen TVSDK API:er för att konfigurera spelarens videospårningsfunktioner.

   * **VisitorID-bibliotek** - Identifierar unikt besökarna på den webbsida som är värd för videospelaren.

   >[!IMPORTANT]
   >
   >Den inbyggda funktionen för videospårning i TVSDK är beroende av en korrekt konfigurerad `AppMeasurement` -instans. Spårningselementen förutsätter att `AppMeasurement` biblioteket har redan instansierats och konfigurerats innan videospårning konfigureras och aktiveras. Funktioner för videospårning i TVSDK är beroende av att det finns en fullt fungerande och korrekt konfigurerad instans av `AppMeasurement` bibliotek.

1. Konfigurera videoanalysrapporter på serversidan med Adobe Analytics Admin Tools.
