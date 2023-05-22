---
title: Java-systemegenskaper
description: Java-systemegenskaper
copied-description: true
exl-id: 3fac8fac-7c71-4638-a671-eecc203dc871
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Java-systemegenskaper {#java-system-properties}

Följande två Java-systemegenskaper kan anges för att ändra platsen för licensserverns konfiguration och loggfiler:

* *LicenseServer.ConfigRoot* — Katalog som innehåller alla konfigurationsfiler för licensservern. Mer information om innehållet i dessa filer finns i &quot;[Konfigurationsfiler för licensserver](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Om den inte anges är standardvärdet *CATALINA_BASE/licensserver*.
* *LicenseServer.LogRoot* — Katalog för mappen &quot;logs&quot;, där licensserverns programloggar skrivs. Om den inte anges är standardvärdet *LicenseServer.ConfigRoot*.

Om du använder [!DNL catalina.bat] eller [!DNL catalina.sh] för att starta Tomcat kan dessa systemegenskaper enkelt anges med `JAVA_OPTS` systemvariabel. Alla Java-alternativ som anges här kommer att användas när Tomcat startas. Ange till exempel:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
