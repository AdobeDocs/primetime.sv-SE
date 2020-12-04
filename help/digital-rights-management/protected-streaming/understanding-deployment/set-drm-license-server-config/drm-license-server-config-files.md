---
seo-title: Konfigurationsfiler för licensserver
title: Konfigurationsfiler för licensserver
uuid: 7c7e0f76-2ced-45af-9542-99e06ec31cda
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
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
