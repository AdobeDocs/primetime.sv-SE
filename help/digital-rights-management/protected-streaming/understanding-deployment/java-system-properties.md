---
description: Det finns flera Java System-egenskaper som du kan konfigurera på licensservern för att styra platsen för konfigurations- och loggfiler.
title: Java-systemegenskaper
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Java-systemegenskaper{#java-system-properties}

Det finns flera Java System-egenskaper som du kan konfigurera på licensservern för att styra platsen för konfigurations- och loggfiler.

Du kan även konfigurera följande Java-systemegenskaper:

* *`LicenseServer.ConfigRoot`* — Namnet på den katalog som innehåller licensserverns konfigurationsfiler.

   Mer information om innehållet i dessa filer finns i *Konfigurationsfiler för licensservern*. Om den inte är konfigurerad är standardvärdet `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot*  - Namnet på  [!DNL logs] katalogen där licensserverns programloggar finns. Om du inte har ändrat namnet på den här katalogen konfigureras namnet på den här katalogen som *LicenseServer.ConfigRoot* som standard.

Om du använder filen [!DNL catalina.bat] eller [!DNL catalina.sh] för att starta Tomcat kan du konfigurera systemegenskaperna med miljövariabeln `JAVA_OPTS`. Alla Java-alternativ som du konfigurerar tillämpas automatiskt när Tomcat startas.

Du kan till exempel konfigurera miljövariabeln `JAVA_OPTS` enligt följande:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

