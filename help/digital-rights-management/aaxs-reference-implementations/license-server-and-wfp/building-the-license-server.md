---
seo-title: Skapar licensservern
title: Skapar licensservern
uuid: d7ca8a8f-c778-41a2-b823-93fac9ab07c5
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Skapar licensservern {#building-the-license-server}

Referensimplementeringslicensservern innehåller WAR-filer för distribution av licensservern. Den innehåller även källkoden för licensservern och ett Ant-byggskript (Reference Implementation\Server\refimpl\build-refimpl.xml) så att du enkelt kan ändra koden.

>[!NOTE]
>
>Det här steget behövs bara om du vill ändra källkoden. I utvärderingssyfte kan du hoppa över det här steget och använda WAR-filerna som de levererats.

Innan du kör Ant-skriptet ändrar du skriptet för att ange platser för Adobe Access SDK, Tomcat, MySQL och Log4J. Öppna build-refimpl.xml i en textredigerare och redigera värdena för egenskaperna `sdkdir, tomcatdir, mysqldir, and log4jdir`. Om du vill kompilera källkoden och skapa WAR-filerna för referensimplementeringen kör du skriptet med `ant -f build-refimpl.xml all` i katalogen som innehåller Ant-skriptet. När skriptet är klart skapas en [!DNL refimpl-build/wars]-katalog som innehåller WAR-serverfilerna.
