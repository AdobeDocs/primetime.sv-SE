---
description: Använd Adobe Primetime DRM API:er för att verifiera signaturen om du vill förbruka lokalt genererade listor över återkallade certifikat (CRL:er) och principuppdateringslistor.
title: Använda lokalt genererade listor över återkallade certifikat
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Använda lokalt genererade listor över återkallade certifikat {#consuming-locally-generated-crls}

Använd Adobe Primetime DRM API:er för att verifiera signaturen om du vill förbruka lokalt genererade listor över återkallade certifikat (CRL:er) och principuppdateringslistor.

Följande API:er kontrollerar att listorna inte har manipulerats och att listorna har signerats av rätt licensserver:

* Utlysning [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) för att kontrollera signaturen innan du anger [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) till alla API:er.

   Mer information finns i [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Utlysning [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) för att kontrollera signaturen innan du anger `PolicyUpdateList` till alla API:er.

   Mer information finns i [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

