---
seo-title: Översikt
title: Översikt
uuid: f4ae10ca-6e2a-4313-80a0-4c7377dba000
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Översikt{#overview}

För att kunna utfärda licenser till klienter måste du distribuera en Adobe Access-licensserver. Licensservern använder Adobe® Access™ SDK för följande:

* Bearbeta autentiseringsbegäranden om autentisering av användarnamn/lösenord stöds.
* Bearbeta licensbegäranden
* Process Get Server Version-begäranden - Alla servrar måste implementera stöd för den här typen av begäran.
* Bearbeta begäran om domänregistrering - behövs bara om du implementerar en domänserver.
* Bearbeta begäran om avregistrering av domän - behövs bara om du implementerar en domänserver.
* Processsynkronisering - Krävs endast om licenserna anger synkroniseringskrav.

Dessutom måste servern tillhandahålla affärslogik för autentisering av användare, avgöra om användare har behörighet att visa innehåll och eventuellt spåra licensanvändning.

Mer information om Java API som diskuteras i det här kapitlet finns i *API-referens för Adobe Access*.
