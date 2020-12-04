---
seo-title: Felsökning
title: Felsökning
uuid: b7a41ea7-86c5-442c-b751-86a9055c5e35
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
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
