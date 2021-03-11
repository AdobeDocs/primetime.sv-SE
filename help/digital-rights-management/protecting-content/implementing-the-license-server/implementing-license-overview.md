---
title: Licensserver - översikt
description: Licensserver - översikt
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Översikt {#license-server-overview}

Innan du kan utfärda licenser till klienter måste du distribuera en Adobe Primetime DRM-licensserver. Licensservern använder Primetimes DRM SDK för att utföra ett antal åtgärder.

Så här implementerar du en licensserver:

* Bearbeta autentiseringsbegäranden om autentisering av användarnamn/lösenord stöds.
* Bearbeta licensbegäranden
* Process Get Server Version-begäranden - Alla servrar måste implementera stöd för den här typen av begäran.
* Bearbeta begäran om domänregistrering - Krävs endast om du implementerar en domänserver.
* Bearbeta begäran om avregistrering av domän - Krävs endast om du implementerar en domänserver.
* Processsynkronisering - Krävs endast om licenserna anger synkroniseringskrav.

Dessutom måste servern tillhandahålla affärslogik för autentisering av användare, avgöra om användare har behörighet att visa innehåll och eventuellt spåra licensanvändning.

Mer information om Java API finns i *API-referens för Adobe Primetime DRM*.
