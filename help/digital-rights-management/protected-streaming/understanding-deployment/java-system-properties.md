---
description: Det finns flera Java System-egenskaper som du kan konfigurera på licensservern för att styra platsen för konfigurations- och loggfiler.
title: Java-systemegenskaper
exl-id: 08fe6910-9d58-41c3-91d3-514406bedf05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Java-systemegenskaper{#java-system-properties}

Det finns flera Java System-egenskaper som du kan konfigurera på licensservern för att styra platsen för konfigurations- och loggfiler.

Du kan även konfigurera följande Java-systemegenskaper:

* *`LicenseServer.ConfigRoot`* — Namnet på den katalog som innehåller licensserverns konfigurationsfiler.

   Se *Konfigurationsfiler för licensserver* om du vill ha information om innehållet i dessa filer. Om den inte är konfigurerad är standardvärdet `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot* — Namn på [!DNL logs] katalog där licensserverns programloggar finns. Om du inte har ändrat namnet på den här katalogen konfigureras namnet på den här katalogen som *LicenseServer.ConfigRoot* som standard.

Om du använder [!DNL catalina.bat] eller [!DNL catalina.sh] för att starta Tomcat kan du konfigurera systemegenskaperna med `JAVA_OPTS` systemvariabel. Alla Java-alternativ som du konfigurerar tillämpas automatiskt när Tomcat startas.

Du kan till exempel konfigurera `JAVA_OPTS` miljövariabel enligt följande:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
