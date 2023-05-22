---
title: Konfigurera SSL på BEES-servern
description: Konfigurera SSL på BEES-servern
copied-description: true
exl-id: 6823a71c-3be6-4c07-a3e6-e16bd931deaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# Konfigurera SSL på BEES-servern {#configure-ssl-on-your-bees-server}

1. Ange SSL-servercertifikatet till den Adobe-kontakt som skickade programvaran.

   Certifikatet läggs till som ett betrott certifikat i DRM-förtroendearkivet i Primetime Cloud.
1. Så här aktiverar du klientautentisering för SSL-anslutningen (inaktiverad i den här versionen):
   1. Lägg till `[!DNL clouddrm-transport.cer]` och `[!DNL AdobeFlashAccessIntermediateCA.cer]` certifikat till förtroendearkivet som används för klientautentisering.
   1. Aktivera klientautentisering i SSL-konfigurationen.
