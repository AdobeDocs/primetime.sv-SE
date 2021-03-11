---
description: Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.
title: Videoanalys
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Videoanalys{#video-analytics}

Du kan spåra videoanvändning genom att integrera TVSDK med Adobe Analytics.

Videospårning i TVSDK använder tjänsten **Adobe Analytics Video Essentials**, som tillhandahåller videointeraktionsstatistik, som videovisningar, färdiga videovisningar, annonsvisningar, hur lång tid som har ägnats åt video och så vidare. Mer information om den här tjänsten får du av Adobe.

Följande procedur sammanfattar stegen som krävs för att aktivera videospårning i spelaren:

1. Initiera och/eller konfigurera följande videospårningskomponenter:

   * **AppMeasurement-bibliotek**  - Innehåller låg nivå för kärnlogik för datainsamling. Det är här som videons pulsslagdata samlas in och skickas över nätverket.
   * **Bibliotek**  med pulsslag i video - Innehåller kärnlogik för datainsamling med pulsslag i video. Biblioteket för videohjärtslag har åtkomst till en delmängd av biblioteks-API:erna för `AppMeasurement`.

      >[!TIP]
      >
      >Din app interagerar inte direkt med videons hjärtslagskod. I stället använder appen TVSDK API:er för att konfigurera spelarens videospårningsfunktioner.

   * **VisitorID Library**  - Identifierar unikt besökare på den webbsida där videospelaren finns.
   >[!IMPORTANT]
   >
   >Den inbyggda videospårningsfunktionen i TVSDK är beroende av en korrekt konfigurerad `AppMeasurement`-instans. Spårningselementen förutsätter att `AppMeasurement`-biblioteket redan har instansierats och konfigurerats innan videospårning konfigureras och aktiveras. Funktionerna för videospårning i TVSDK är beroende av att det finns en fullt fungerande och korrekt konfigurerad instans av `AppMeasurement`-biblioteket.

1. Konfigurera videoanalysrapporter på serversidan med Adobe Analytics Admin Tools.

