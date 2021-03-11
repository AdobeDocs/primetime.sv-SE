---
title: Uppgraderar klienter
description: Uppgraderar klienter
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Uppgraderar klienter{#upgrading-clients}

Om en FMRMS 1.x-klient kontaktar en Adobe Access-server måste servern uppmana klienten att uppgradera.

* Begäranhanterarklassen är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x content*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   Till skillnad från andra hanterare för Adobe Access-begäranden ger hanteraren inte åtkomst till någon begärandeinformation och kräver att några svarsdata ställs in. Skapa en instans av `FMRMSv1RequestHandler` och anropa sedan `close()`