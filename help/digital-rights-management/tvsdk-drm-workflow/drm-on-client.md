---
seo-title: Primetime DRM på klienten
title: Primetime DRM på klienten
uuid: 472180ad-6596-4a24-aa51-7909a75a5e10
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---


# Primetime DRM på klienten{#primetime-drm-on-the-client}

Ett Primetime TVSDK-program som spelar upp skyddat innehåll måste först anropa Primetimes DRM API:er för att initiera arbetsflödet för licensförbrukning och uppspelning av skyddat innehåll. I det här arbetsflödet skapar Primetime DRM på klienten en licensbegäran från metadata för det skyddade innehållet och skickar den sedan till Primetimes DRM-licensserver.

Innan licensbegäran utfärdas kan klienten välja att utföra nödvändig autentisering/auktorisering (beroende på dina affärsregler).
