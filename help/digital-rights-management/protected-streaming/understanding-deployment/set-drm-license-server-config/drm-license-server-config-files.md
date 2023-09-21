---
title: Konfigurationsfiler för licensserver
description: Konfigurationsfiler för licensserver
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
