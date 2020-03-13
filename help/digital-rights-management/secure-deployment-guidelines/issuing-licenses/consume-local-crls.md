---
description: Om du vill förbruka lokalt genererade listor över återkallade certifikat (CRL) och principuppdateringslistor använder du Adobe Primetimes DRM API:er för att verifiera signaturen.
seo-description: Om du vill förbruka lokalt genererade listor över återkallade certifikat (CRL) och principuppdateringslistor använder du Adobe Primetimes DRM API:er för att verifiera signaturen.
seo-title: Använda lokalt genererade listor över återkallade certifikat
title: Använda lokalt genererade listor över återkallade certifikat
uuid: 2e20b8ca-8606-4c27-b585-2f020b93be32
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Använda lokalt genererade listor över återkallade certifikat {#consuming-locally-generated-crls}

Om du vill förbruka lokalt genererade listor över återkallade certifikat (CRL) och principuppdateringslistor använder du Adobe Primetimes DRM API:er för att verifiera signaturen.

Följande API:er kontrollerar att listorna inte har manipulerats och att listorna har signerats av rätt licensserver:

* Anropa [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) för att kontrollera signaturen innan du skickar [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) till några API:er.

   Mer information finns i [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).

* Anropa [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) för att kontrollera signaturen innan du skickar informationen `PolicyUpdateList` till några API:er.

   Mer information finns i [PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html).

