---
seo-title: Distribuera certifikat - översikt
title: Distribuera certifikat - översikt
uuid: e6413f9f-69a5-4881-bb13-47a80cf32a48
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Översikt {#deploy-certificates-overview}

Om du vill lägga till certifikat i DRM-egenskapsfilerna för Adobe Primetime konverterar du PKCS#7-filen till en PFX-fil med den privata nyckeln och skapar antingen en PEM-fil eller en DER-fil.

* När en autentiseringsuppgift (certifikat och privat nyckel) krävs, kräver kommandoradsverktygen för Primetime DRM och Adobe HTTP Dynamic Streaming Packager en PFX-fil. SDK, referensimplementering och Primetime DRM-servern för skyddad direktuppspelning kan acceptera en PFX-fil och kan även använda autentiseringsuppgifter som lagras på en HSM.
* När bara ett certifikat krävs kan de flesta DRM-komponenter i Primetime använda en PEM-fil, en DER-fil eller ett certifikat på en HSM. Adobe HTTP Dynamic Streaming Packager accepterar endast DER-filer för certifikat.