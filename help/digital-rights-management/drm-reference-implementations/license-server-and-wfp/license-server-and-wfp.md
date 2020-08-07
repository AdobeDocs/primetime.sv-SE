---
description: Referensimplementeringsservern kan hjälpa dig att skapa en fullt fungerande licensserver som använder alla funktioner i Adobe Primetime DRM Java SDK.
seo-description: Referensimplementeringsservern kan hjälpa dig att skapa en fullt fungerande licensserver som använder alla funktioner i Adobe Primetime DRM Java SDK.
seo-title: Licensserver
title: Licensserver
uuid: 39cb0d0f-f3dc-48e9-b6fd-6960a9ade291
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Licensserver {#license-server}

Referensimplementeringsservern kan hjälpa dig att skapa en fullt fungerande licensserver som använder alla funktioner i Adobe Primetime DRM Java SDK.

I den här implementeringen autentiseras användare baserat på användarposter i en databas. Servern innehåller demonstrationslogik för att utfärda licenser och erbjuder kompatibilitetsstöd för Flash Media Rights Management Server 1.0 och 1.5.

## Krav för licensservern {#license-server-requirements}

Krav för licensservern:

* Installera Tomcat 6.0 eller senare
* Installera en databas, t.ex. MySQL (finns på dvd:n, i [!DNL Third Party\MySQL])
* Kontrollera att du har Java 1.6 eller senare installerat
* Kontrollera att du har Ant 1.8 eller senare för att köra exempelbyggskript

När du har installerat Tomcat och MySQL kontaktar du Adobe för att få de DRM-autentiseringsuppgifter som krävs.

## Bygg licensservern {#build-the-license-server}

>[!NOTE]
>
>Du behöver bara skapa licensservern om du tänker ändra källkoden. I utvärderingssyfte kan du helt enkelt använda WAR-filerna som de levererats.

Referensimplementeringslicensservern innehåller all licensserverns källkod ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), tillsammans med ett Ant-byggskript ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) som du kan använda för att anpassa licensservern efter dina affärsbehov.

1. Ändra Ant-byggskriptet för att ange platser för Primetime DRM SDK, Tomcat, MySQL och Log4J.

   Öppna [!DNL build-refimpl.xml] filen i en textredigerare och ange följande egenskapsvärden:

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. Kör Ant-byggskriptet med egenskapen `all` , i katalogen där Ant-byggskriptet finns.

   ```
   ant -f build-refimpl.xml all
   ```

   Ant-byggskriptet skapar en [!DNL refimpl-build/wars] katalog som innehåller serverns WAR-filer.
