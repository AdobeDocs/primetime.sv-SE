---
title: Konfigurationsfiler för licensserver
description: Konfigurationsfiler för licensserver
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

Mer information om hur du krypterar lösenord finns i *Lösenordssparare*.
