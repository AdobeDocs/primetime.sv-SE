---
description: Du kan spåra videoanvändning genom att integrera Browser TVSDK med Adobe Analytics.
title: Videoanalys
exl-id: b6fb39a9-6cb8-4498-a9fa-0ea19af52a58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Videoanalys{#video-analytics}

Du kan spåra videoanvändning genom att integrera Browser TVSDK med Adobe Analytics.

Videospårning i webbläsarens TVSDK använder **Adobe Analytics Video Essentials** som tillhandahåller interaktionsstatistik för video, som videovisningar, kompletta videofilmer, annonsvisningar, tidsåtgång för video och så vidare. Mer information om den här tjänsten får du av Adobe.

Följande procedur sammanfattar stegen som krävs för att aktivera videospårning i spelaren:

1. Initiera och/eller konfigurera följande videospårningskomponenter:

   * **AppMeasurement-bibliotek** - Innehåller den grundläggande logiken för datainsamling på låg nivå. Det är här som videons pulsslagdata samlas in och skickas över nätverket.
   * **Bibliotek för videohjärtslag** - Innehåller kärnlogik för datainsamling med pulsslag. Biblioteket för videohjärtslag har åtkomst till en delmängd av API:erna för AppMeasurement-biblioteket.

      >[!TIP]
      >
      >Din app interagerar inte direkt med videons hjärtslagskod. I stället använder appen webbläsarens TVSDK API:er för att konfigurera spelarens videospårningsfunktioner.

   * **VisitorID-bibliotek** - Identifierar unikt besökarna på den webbsida som är värd för videospelaren.
   >[!IMPORTANT]
   >
   >Den inbyggda funktionen för videospårning i Browser TVSDK är beroende av en korrekt konfigurerad AppMeasurement-instans. Spårningselementen förutsätter att AppMeasurement-biblioteket redan har instansierats och konfigurerats innan videospårning konfigureras och aktiveras. Funktionerna för spårning av video i webbläsare-TVSDK är beroende av att det finns en fullt fungerande och korrekt konfigurerad instans av AppMeasurement-biblioteket.

1. Konfigurera videoanalysrapporter på serversidan med Adobe Analytics Admin Tools.
