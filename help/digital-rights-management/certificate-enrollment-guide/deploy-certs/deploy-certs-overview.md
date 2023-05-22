---
title: Distribuera certifikatöversikt
description: Distribuera certifikatöversikt
copied-description: true
exl-id: 45a4bc7e-f987-4b9a-885d-d989d09566c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Översikt {#deploy-certificates-overview}

Om du vill lägga till certifikat till Adobe Primetime DRM-egenskapsfilerna konverterar du PKCS#7-filen till en PFX-fil med den privata nyckeln och skapar antingen en PEM-fil eller en DER-fil.

* När en autentiseringsuppgift (certifikat och privat nyckel) krävs kräver kommandoradsverktygen för DRM och paketeraren för Adobe HTTP Dynamic Streaming en PFX-fil. SDK, referensimplementering och Primetime DRM-servern för skyddad direktuppspelning kan acceptera en PFX-fil och kan även använda autentiseringsuppgifter som lagras på en HSM.
* När bara ett certifikat krävs kan de flesta DRM-komponenter i Primetime använda en PEM-fil, en DER-fil eller ett certifikat på en HSM. Adobe HTTP Dynamic Streaming-paketeraren accepterar endast DER-filer för certifikat.
