---
title: Uppgraderar klienter
description: Uppgraderar klienter
copied-description: true
exl-id: 0476c9ef-3622-4bc5-bb24-f8543470b7d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Uppgraderar klienter{#upgrading-clients}

Om en FMRMS 1.x-klient kontaktar en Adobe Access-server måste servern uppmana klienten att uppgradera.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x-innehåll*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   Till skillnad från andra hanterare för Adobe Access-begäranden ger hanteraren inte åtkomst till någon begärandeinformation och kräver att några svarsdata ställs in. Skapa en instans av `FMRMSv1RequestHandler`och sedan ringa `close()`
