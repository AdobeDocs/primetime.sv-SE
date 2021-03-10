---
title: Distribuera certifikatöversikt
description: Distribuera certifikatöversikt
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Översikt {#deploy-certificates-overview}

Om du vill lägga till certifikat till Adobe Primetime DRM-egenskapsfilerna konverterar du PKCS#7-filen till en PFX-fil med den privata nyckeln och skapar antingen en PEM-fil eller en DER-fil.

* När en autentiseringsuppgift (certifikat och privat nyckel) krävs kräver kommandoradsverktygen för DRM och paketeraren för Adobe HTTP Dynamic Streaming en PFX-fil. SDK, referensimplementering och Primetime DRM-servern för skyddad direktuppspelning kan acceptera en PFX-fil och kan även använda autentiseringsuppgifter som lagras på en HSM.
* När bara ett certifikat krävs kan de flesta DRM-komponenter i Primetime använda en PEM-fil, en DER-fil eller ett certifikat på en HSM. Adobe HTTP Dynamic Streaming-paketeraren accepterar endast DER-filer för certifikat.