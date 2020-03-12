---
seo-title: Java-systemegenskaper
title: Java-systemegenskaper
uuid: ad1f3d9b-7d95-4e19-a0f8-fd7d4dd4dc32
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Java-systemegenskaper {#java-system-properties}

Följande två Java-systemegenskaper kan anges för att ändra platsen för licensserverns konfiguration och loggfiler:

* *LicenseServer.ConfigRoot* - Katalog som innehåller alla konfigurationsfiler för licensservern. Mer information om innehållet i dessa filer finns i&quot;[Licensserverkonfigurationsfiler](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Om den inte anges är standardinställningen *CATALINA_BASE/licensserver*.
* *LicenseServer.LogRoot* - Katalog över mappen &quot;logs&quot;, där licensserverns programloggar skrivs. Om den inte anges är standardvärdet *LicenseServer.ConfigRoot*.

Om du använder [!DNL catalina.bat] eller [!DNL catalina.sh] startar Tomcat kan du enkelt ange dessa systemegenskaper med hjälp av `JAVA_OPTS` systemvariabeln. Alla Java-alternativ som anges här kommer att användas när Tomcat startas. Ange till exempel:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

