---
seo-title: Konfigurera SSL på BEES-servern
title: Konfigurera SSL på BEES-servern
uuid: 041a106e-8b21-4018-815d-b7ea48c3de03
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Konfigurera SSL på BEES-servern {#configure-ssl-on-your-bees-server}

1. Ange SSL-servercertifikatet till den Adobe-kontakt som tillhandahöll programvaran.

   Certifikatet läggs till som ett betrott certifikat i DRM-förtroendearkivet i Primetime Cloud.
1. Så här aktiverar du klientautentisering för SSL-anslutningen (inaktiverad i den här versionen):
   1. Lägg till certifikat `[!DNL clouddrm-transport.cer]` och `[!DNL AdobeFlashAccessIntermediateCA.cer]` certifikat i förtroendearkivet som används för klientautentisering.
   1. Aktivera klientautentisering i SSL-konfigurationen.
