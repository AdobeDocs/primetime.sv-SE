---
title: Versionsinformation om Adobe Primetime Concurrency Monitoring 2.3.2
description: Versionsinformation om Adobe Primetime Concurrency Monitoring 2.3.2
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Versionsinformation om Adobe Primetime Concurrency Monitoring 2.3.2 {#cm-232}

Den här sidan beskriver nya funktioner, ändringar och kända fel i den här versionen:

Releasedatum: 2015-12-11

## Nya funktioner och förbättringar {#new-features}

* Nya uppdelningar finns i användningsrapporter. De nya uppdelningarna är tillgängliga om programmet som är integrerat med Concurrency Monitoring skickar anpassade metadata.
   * program - det program-ID som rapporteras i anrops-URL
   * mvpd - det MVPD som rapporterades i anrops-URL
   * kanal - den anpassade metadatakanalen
   * platform - det anpassade metadataprogrammetPlatform
* Nya mätvärden relaterade till **varaktighet för ström** finns i användningsrapporterna. De nya mätvärdena kan användas för att skapa ett histogram med flödeslängd. Följande intervaller i minuter är tillgängliga:
   * duration_0-15
   * duration_15-30
   * duration_30-60
   * duration_60-120
   * duration_over-120

## Felkorrigeringar {#bug-fixes}

Ej tillämpligt

## Kända fel {#known-issues}

Ej tillämpligt
