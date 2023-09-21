---
title: Felsökning
description: Felsökning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# Felsökning{#troubleshooting}

* För vissa äldre enheter som kör API-nivå 10 eller äldre kan logcat inte öppna loggenheten på grund av ett behörighetsproblem. Följande undantag visas: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Lösning:**

   1. Öppna [!DNL AndroidManifest.xml] under [!DNL CatalogActivity] i arbetsytan.

   1. Lägg till följande behörighet i [!DNL `AndroidManfest.xml`] fil:

      ```
      android.permission.READ_LOGS
      ```
