---
seo-title: Förbruka lokalt genererade listor över återkallade certifikat
title: Förbruka lokalt genererade listor över återkallade certifikat
uuid: 5a4519b8-6dbd-4921-9048-6c9f67aae18d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Förbruka lokalt genererade listor över återkallade certifikat{#consume-locally-generated-crls}

Om du vill förbruka lokalt genererade listor över återkallade certifikat (CRL) och principuppdateringslistor använder du API:er för Adobe Access för att verifiera signaturen. API:erna kontrollerar att listorna inte har manipulerats och att de har signerats av rätt licensserver.

* Anropa `RevocationList.verifySignature` för att kontrollera signaturen innan RevocationList skickas till några API:er.

   Mer information finns `RevocationListFactory` i API-referens *för* Adobe Access.

* Anropa `PolicyUpdateList.verifySignature`för att kontrollera signaturen innan du skickar informationen `PolicyUpdateList` till några API:er.

   Mer information finns `PolicyUpdateList` i API-referens *för* Adobe Access.

