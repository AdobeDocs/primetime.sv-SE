---
title: Konfigurationsfiler för licensserver
description: Konfigurationsfiler för licensserver
copied-description: true
exl-id: d48e88a4-caae-4f4e-b870-38da4f3a715e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Konfigurationsfiler för licensserver{#license-server-configuration-files}

Adobe Primetime DRM Server for Protected Streaming kräver följande typer av konfigurationsfiler:

* Global konfigurationsfil ( [!DNL flashaccess-global.xml])
* Konfigurationsfil för klientorganisation för varje klientorganisation ( [!DNL flashaccess-tenant.xml])

När du är klar med redigeringen av konfigurationsfilerna rekommenderar Adobe att du använder verktygen i Primetime DRM Server for Protected Streaming för att verifiera att filerna är välformade.

Se *Konfigurationsvaliderare*.

Om du inte vill att lösenord ska vara tillgängliga i klartext i konfigurationsfilerna måste du kryptera alla lösenord som du har angett i de globala konfigurationsfilerna och klientkonfigurationsfilerna med hjälp av verktyget Scrambler som Adobe har tillhandahållit.

Se *Lösenordsfasare* om du vill ha mer information om hur du krypterar lösenord.
