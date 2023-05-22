---
title: Felsökning
description: Felsökning
copied-description: true
exl-id: 618b1e19-d25d-435d-b118-b43455bde974
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# Felsökning{#troubleshooting}

* För vissa äldre enheter som kör API-nivå 10 eller äldre kan logcat inte öppna loggenheten på grund av ett behörighetsproblem. Följande undantag visas: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Tillfällig lösning:**

   1. Öppna [!DNL AndroidManifest.xml] under [!DNL CatalogActivity] -projekt på arbetsytan.

   1. Lägg till följande behörighet i [!DNL `AndroidManfest.xml`] fil:

      ```
      android.permission.READ_LOGS
      ```
