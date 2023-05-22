---
title: Översikt
description: Översikt
copied-description: true
exl-id: 7327386b-e796-4fa5-bda4-cacc612a9d1f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
* Bearbeta begäran om avregistrering av domän - Krävs endast om en domänserver implementeras.
* Processsynkronisering - Krävs endast om licenserna anger synkroniseringskrav.

Dessutom måste servern tillhandahålla affärslogik för autentisering av användare, avgöra om användare har behörighet att visa innehåll och eventuellt spåra licensanvändning.

Mer information om Java API som beskrivs i det här kapitlet finns i *API-referens för Adobe Access*.
