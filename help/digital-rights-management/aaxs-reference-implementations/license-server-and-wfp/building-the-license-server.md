---
title: Skapar licensservern
description: Skapar licensservern
copied-description: true
exl-id: 0535f1e4-9f63-47a0-b55c-45c32ba0d15e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Skapar licensservern {#building-the-license-server}

Referensimplementeringslicensservern innehåller WAR-filer för distribution av licensservern. Den innehåller även källkoden för licensservern och ett Ant-byggskript (Reference Implementation\Server\refimpl\build-refimpl.xml) så att du enkelt kan ändra koden.

>[!NOTE]
>
>Det här steget behövs bara om du vill ändra källkoden. I utvärderingssyfte kan du hoppa över det här steget och använda WAR-filerna som de levererats.

Innan du kör Ant-skriptet ändrar du skriptet för att ange platser för Adobe Access SDK, Tomcat, MySQL och Log4J. Öppna build-refimpl.xml i en textredigerare och redigera egenskapsvärdena `sdkdir, tomcatdir, mysqldir, and log4jdir`. Om du vill kompilera källkoden och skapa WAR-filerna för referensimplementeringen kör du skriptet med `ant -f build-refimpl.xml all` i katalogen som innehåller Ant-skriptet. När skriptet är klart, [!DNL refimpl-build/wars] katalog som innehåller WAR-serverfilerna skapas.
