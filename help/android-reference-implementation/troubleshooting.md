---
title: Felsökning
description: Felsökning
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---


# Felsökning{#troubleshooting}

* För vissa äldre enheter som kör API-nivå 10 eller äldre kan logcat inte öppna loggenheten på grund av ett behörighetsproblem. Följande undantag visas: `java.lang.Exception: logcat returns error: Unable to open log device '/dev/log/main': Permission denied` **Tillfällig lösning:**

   1. Öppna [!DNL AndroidManifest.xml] under [!DNL CatalogActivity]-projektet på arbetsytan.

   1. Lägg till följande behörighet i [!DNL `AndroidManfest.xml`]-filen:

      ```
      android.permission.READ_LOGS
      ```
