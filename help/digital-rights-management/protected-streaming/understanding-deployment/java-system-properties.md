---
description: Det finns flera Java System-egenskaper som du kan konfigurera på licensservern för att styra platsen för konfigurations- och loggfiler.
seo-description: Det finns flera Java System-egenskaper som du kan konfigurera på licensservern för att styra platsen för konfigurations- och loggfiler.
seo-title: Java-systemegenskaper
title: Java-systemegenskaper
uuid: d8c72359-bf61-47e0-9cd5-b21225d5fe49
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Java-systemegenskaper{#java-system-properties}

Det finns flera Java System-egenskaper som du kan konfigurera på licensservern för att styra platsen för konfigurations- och loggfiler.

Du kan även konfigurera följande Java-systemegenskaper:

* *`LicenseServer.ConfigRoot`* — Namnet på den katalog som innehåller licensserverns konfigurationsfiler.

   Se Konfigurationsfiler *för* licensserver för mer information om innehållet i dessa filer. Om den inte är konfigurerad är standardvärdet `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot* - Namnet på den [!DNL logs] katalog där licensserverns programloggar finns. Om du inte har ändrat namnet på den här katalogen konfigureras namnet på den här katalogen som *LicenseServer.ConfigRoot* som standard.

Om du använder [!DNL catalina.bat] - eller [!DNL catalina.sh] -filen för att starta Tomcat kan du konfigurera systemegenskaperna med `JAVA_OPTS` systemvariabeln. Alla Java-alternativ som du konfigurerar tillämpas automatiskt när Tomcat startas.

Du kan till exempel konfigurera `JAVA_OPTS` miljövariabeln på följande sätt:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

