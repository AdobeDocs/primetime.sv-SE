---
title: Generera listor över återkallade certifikat som kompletterar dem som Adobe har publicerat
description: Generera listor över återkallade certifikat som kompletterar dem som Adobe har publicerat
copied-description: true
exl-id: 05dc2159-fa7f-4772-9f25-c89370b4981e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Generera listor över återkallade certifikat som kompletterar dem som Adobe har publicerat{#generate-crls-to-supplement-those-published-by-adobe}

Med Adobe Access kan du skapa listor över återkallade certifikat som ett komplement till den lista över återkallade certifikat som Adobe har publicerat. Adobe Access SDK kontrollerar och tillämpar Adobe CRL:er, men du kan inte tillåta ytterligare klientdatorer genom att skapa en CRL som återkallar ytterligare datorautentiseringsuppgifter. För att göra detta måste du skicka CRL:en till Adobe Access SDK. När du sedan utfärdar en licens kontrollerar SDK både Adobe CRL och din egen CRL.

Mer information om hur du genererar CRL:er finns i `RevocationListFactory` in *API-referens för Adobe Access*.
