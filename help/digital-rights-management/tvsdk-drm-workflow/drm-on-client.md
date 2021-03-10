---
title: Primetime DRM på klienten
description: Primetime DRM på klienten
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Primetime DRM på klienten{#primetime-drm-on-the-client}

Ett Primetime TVSDK-program som spelar upp skyddat innehåll måste först anropa Primetimes DRM API:er för att initiera arbetsflödet för licensförbrukning och uppspelning av skyddat innehåll. I det här arbetsflödet skapar Primetime DRM på klienten en licensbegäran från metadata för det skyddade innehållet och skickar den sedan till Primetimes DRM-licensserver.

Innan licensbegäran utfärdas kan klienten välja att utföra nödvändig autentisering/auktorisering (beroende på dina affärsregler).
