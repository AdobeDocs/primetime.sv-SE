---
title: Använd Adobe Media Server
description: Använd Adobe Media Server
copied-description: true
exl-id: bb0b12f0-cd33-4a8a-8466-ae0e35cb1641
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# Använd Adobe Media Server {#use-adobe-media-server}

Vissa kunder kanske redan använder Adobe Media Server och vill underhålla innehållsleveransmodellen. Om så är fallet kan de DRM-specifika data som krävs för Primetime Cloud samlas in från någon av konfigurationsfilerna som ingår i paketet för att fylla i XML-konfigurationen för JIT (Just In Time) för AMS.

Till exempel:

```xml
<?xml version="1.0"?>
<Application>
  <HDS>
    <HLS>
      <Encryption enabled="true" protection-scheme="AdobeAccessV4">
        <AdobeAccessV4>
          <ContentID>SampleVideo</ContentID>
          <CommonKeyPath>common-key.bin</CommonKeyPath>
          <LicenseServerURL>
            https://access.adobeprimetime.com/flashaccessserver/axs_prod
          </LicenseServerURL>
          <KeyServerURL>
            https://access.adobeprimetime.com:443/faxsks/axs_prod/key
          </KeyServerURL>
          <TransportCertPath>cert/Cloud DRM-transport.cer</TransportCertPath>
          <LicenseServerCertPath>cert/Cloud DRM-license.cer</LicenseServerCertPath>
          <PackagerCredentialPath>cert-from-adobe.pfx</PackagerCredentialPath>
          <PackagerCredentialPwd>pass-for-cert-from-adobe</PackagerCredentialPwd>
          <PolicyPath>policy_ios_localkeyserver.pol</PolicyPath>
        </AdobeAccessV4>
      </Encryption>
    </HLS>
  </HDS>
</Application>
```
