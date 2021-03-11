---
title: Förbruka lokalt genererade listor över återkallade certifikat
description: Förbruka lokalt genererade listor över återkallade certifikat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Förbruka lokalt genererade listor över återkallade certifikat{#consume-locally-generated-crls}

Om du vill förbruka lokalt genererade listor över återkallade certifikat (CRL) och principuppdateringslistor använder du API:er för Adobe Access för att verifiera signaturen. API:erna kontrollerar att listorna inte har manipulerats och att de har signerats av rätt licensserver.

* Anropa `RevocationList.verifySignature` för att kontrollera signaturen innan du skickar RevocationList till några API:er.

   Mer information finns i `RevocationListFactory` i *API-referens för Adobe Access*.

* Anropa `PolicyUpdateList.verifySignature`för att kontrollera signaturen innan du skickar `PolicyUpdateList` till några API:er.

   Mer information finns i `PolicyUpdateList` i *API-referens för Adobe Access*.

