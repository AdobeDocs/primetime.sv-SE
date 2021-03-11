---
title: Generera listor över återkallade certifikat som kompletterar dem som Adobe har publicerat
description: Generera listor över återkallade certifikat som kompletterar dem som Adobe har publicerat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Generera listor över återkallade certifikat som kompletterar dem som publicerats av Adobe{#generate-crls-to-supplement-those-published-by-adobe}

Med Adobe Access kan du skapa listor över återkallade certifikat som ett komplement till den lista över återkallade certifikat som Adobe har publicerat. Adobe Access SDK kontrollerar och tillämpar Adobe CRL:er, men du kan inte tillåta ytterligare klientdatorer genom att skapa en CRL som återkallar ytterligare datorautentiseringsuppgifter. För att göra detta måste du skicka CRL:en till Adobe Access SDK. När du sedan utfärdar en licens kontrollerar SDK både Adobe CRL och din egen CRL.

Mer information om hur du skapar CRL:er finns i `RevocationListFactory` i *API-referens för Adobe Access*.
