---
title: Förbruka lokalt genererade listor över återkallade certifikat
description: Förbruka lokalt genererade listor över återkallade certifikat
copied-description: true
exl-id: d96418d0-8fd3-4f6d-8480-191fe540080a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Förbruka lokalt genererade listor över återkallade certifikat{#consume-locally-generated-crls}

Om du vill förbruka lokalt genererade listor över återkallade certifikat (CRL) och principuppdateringslistor använder du API:er för Adobe Access för att verifiera signaturen. API:erna kontrollerar att listorna inte har manipulerats och att de har signerats av rätt licensserver.

* Utlysning `RevocationList.verifySignature` för att kontrollera signaturen innan RevocationList skickas till några API:er.

   Mer information finns i `RevocationListFactory` i *API-referens för Adobe Access*.

* Utlysning `PolicyUpdateList.verifySignature`för att kontrollera signaturen innan du anger `PolicyUpdateList` till alla API:er.

   Mer information finns i `PolicyUpdateList` i *API-referens för Adobe Access*.
