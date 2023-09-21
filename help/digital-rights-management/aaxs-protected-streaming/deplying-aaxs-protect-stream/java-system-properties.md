---
title: Java-systemegenskaper
description: Java-systemegenskaper
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Java-systemegenskaper {#java-system-properties}

Följande två Java-systemegenskaper kan anges för att ändra platsen för licensserverns konfiguration och loggfiler:

* *LicenseServer.ConfigRoot* — Katalog som innehåller alla konfigurationsfiler för licensservern. Mer information om innehållet i dessa filer finns i &quot;[Konfigurationsfiler för licensserver](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Om den inte anges är standardvärdet *CATALINA_BASE/licensserver*.
* *LicenseServer.LogRoot* — Katalog för mappen &quot;logs&quot;, där licensserverns programloggar skrivs. Om den inte anges är standardvärdet *LicenseServer.ConfigRoot*.

Om du använder [!DNL catalina.bat] eller [!DNL catalina.sh] för att starta Tomcat kan dessa systemegenskaper enkelt anges med `JAVA_OPTS` miljövariabel. Alla Java-alternativ som anges här kommer att användas när Tomcat startas. Ange till exempel:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
