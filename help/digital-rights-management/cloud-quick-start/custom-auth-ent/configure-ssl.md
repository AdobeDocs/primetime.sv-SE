---
title: Konfigurera SSL på BEES-servern
description: Konfigurera SSL på BEES-servern
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Konfigurera SSL på BEES-servern {#configure-ssl-on-your-bees-server}

1. Ange SSL-servercertifikatet till den Adobe-kontakt som levererade programvaran.

   Certifikatet läggs till som ett betrott certifikat i DRM-förtroendearkivet i Primetime Cloud.
1. Så här aktiverar du klientautentisering för SSL-anslutningen (inaktiverad i den här versionen):
   1. Lägg till `[!DNL clouddrm-transport.cer]` och `[!DNL AdobeFlashAccessIntermediateCA.cer]` certifikat till förtroendearkivet som används för klientautentisering.
   1. Aktivera klientautentisering i SSL-konfigurationen.
