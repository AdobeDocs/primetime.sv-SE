---
seo-title: Uppgraderar klienter
title: Uppgraderar klienter
uuid: 9c9bc7da-2a97-4659-945a-554d778d30a3
translation-type: tm+mt
source-git-commit: 5cf90a75d8805fb64d7d145722ad10a1ce77a14d

---


# Uppgraderar klienter{#upgrading-clients}

Om en FMRMS 1.x-klient kontaktar en Adobe Access-server måste servern uppmana klienten att uppgradera.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* Begärans URL är &quot;*Bas-URL från 1.x-innehåll*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;

   Till skillnad från andra hanterare för Adobe Access-begäranden ger hanteraren inte åtkomst till någon begärandeinformation och kräver att några svarsdata ställs in. Skapa en instans av `FMRMSv1RequestHandler`och anropa sedan `close()`