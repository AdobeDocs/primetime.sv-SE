---
seo-title: Licensserver - översikt
title: Licensserver - översikt
uuid: 8c62376b-b159-4297-9322-75d62947e84e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

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

Mer information om Java API finns i API-referens *för* Adobe Primetime.
