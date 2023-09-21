---
title: Uppgraderar klienter
description: Uppgraderar klienter
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Uppgraderar klienter{#upgrading-clients}

Om en FMRMS 1.x-klient kontaktar en Adobe Access-server måste servern uppmana klienten att uppgradera.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x-innehåll*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

  Till skillnad från andra hanterare för Adobe Access-begäranden ger hanteraren inte åtkomst till någon begärandeinformation och kräver att några svarsdata ställs in. Skapa en instans av `FMRMSv1RequestHandler`och sedan ringa `close()`
