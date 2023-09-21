---
title: Konfigurera Adobe Primetime Ad Insertion
description: Konfigurera Adobe Primetime Ad Insertion
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Konfigurera Adobe Primetime Ad Insertion {#ptai-setup}

Processen för att konfigurera Primetime Ad Insertion är följande:

1. Integrera er annonsserver i Primetime Ad Insertion genom att logga in på Primetimes Ad Insertion-konsol och konfigurera omdirigeringsregler. Mer information finns i [Integrera er annonsserver](/help/primetime-ad-insertion/getting-started/integrate-ad-server.md).

1. Konfigurera kanaler eller plattformar i Primetime Ad Insertion-konsolen för att säkerställa lämpliga rapporteringsdimensioner.

1. Konfigurera och integrera ditt CDN i Primetime Ad Insertion. Mer information finns i [Integrera ditt CDN](integrate-cdn.md).

1. Bestäm om precis-i-tid-annonspaketering krävs för ert annonsarbetsflöde. Kontakta din supportrepresentant på Primetime för att aktivera tjänsten.

1. Uppdatera programmet så att det använder [BOOTSTRAP API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) för att göra och ta emot förfrågningar för Primetime Ad Insertion och konfigurera ditt program så att det stöder dem. Mer information finns i [Annonsspårning](set-up-ad-tracking.md).

1. Testa programmet för att säkerställa korrekt annonsuppspelning med [Felsökningsverktyg](/help/primetime-ad-insertion/performance-monitoring-debugging-reporting/troubleshoot-and-debug.md).

1. Testa applikationerna för att säkerställa korrekt aktivering av annonsspårning och visningssignaler med [Rapportering](/help/primetime-ad-insertion/performance-monitoring-debugging-reporting/reporting-and-billing.md).
