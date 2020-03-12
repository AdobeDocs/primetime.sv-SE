---
seo-title: Generera listor över återkallade certifikat som kompletterar dem som publicerats av Adobe
title: Generera listor över återkallade certifikat som kompletterar dem som publicerats av Adobe
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Generera listor över återkallade certifikat som kompletterar dem som publicerats av Adobe{#generate-crls-to-supplement-those-published-by-adobe}

Med Adobe Access kan du skapa listor över återkallade certifikat som komplement till den lista över återkallade certifikat som publicerats av Adobe. Adobe Access SDK kontrollerar och verkställer Adobes listor över återkallade certifikat (CRL), men du kan neka ytterligare klientdatorer genom att skapa en lista över återkallade certifikat som återkallar ytterligare autentiseringsuppgifter för datorer. För att kunna göra detta måste du skicka CRL:en till Adobe Access SDK. När du sedan utfärdar en licens kontrollerar SDK både Adobe CRL och din egen CRL.

Mer information om hur du genererar CRL finns `RevocationListFactory` i API-referens *för* Adobe Access.
