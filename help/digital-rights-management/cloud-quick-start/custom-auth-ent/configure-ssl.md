---
title: Konfigurera SSL på BEES-servern
description: Konfigurera SSL på BEES-servern
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# Konfigurera SSL på BEES-servern {#configure-ssl-on-your-bees-server}

1. Ange SSL-servercertifikatet till den Adobe-kontakt som skickade programvaran.

   Certifikatet läggs till som ett betrott certifikat i DRM-förtroendearkivet i Primetime Cloud.
1. Så här aktiverar du klientautentisering för SSL-anslutningen (inaktiverad i den här versionen):
   1. Lägg till `[!DNL clouddrm-transport.cer]`- och `[!DNL AdobeFlashAccessIntermediateCA.cer]`-certifikaten i förtroendearkivet som används för klientautentisering.
   1. Aktivera klientautentisering i SSL-konfigurationen.
