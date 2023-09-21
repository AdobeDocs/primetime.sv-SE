---
title: Begär ett certifikat (begärande)
description: Begär ett certifikat (begärande)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Begär ett certifikat (begärande){#request-a-certificate-requester}

1. Logga in på webbplatsen för certifikatregistrering.

   Användaren som begär ett certifikat måste vara en beställare.

1. På fliken Begäran väljer du typ av certifikat (licensserver, Packager eller Transport).

   >[!NOTE]
   >
   >Det här alternativet visas inte för SDK-versionerna för utvärdering och testversion. Dessa SDK-versioner använder ett certifikat.

1. Gör något av följande:

   * Överför CSR-filen.
   * Kopiera CSR-informationen från CSR och klistra in den i formuläret.

     >[!NOTE]
     >
     >Om du vill kopiera CSR-informationen markerar du texten mellan, inte inklusive, den inledande taggen `(-----BEGIN CERTIFICATE REQUEST-----)` och sluttagg `(-----END CERTIFICATE REQUEST-----)`.

1. Klicka på **[!UICONTROL Submit Request]** -knappen.

   Ett e-postmeddelande skickas till kontoadministratören och de sekundära administratörerna för granskning. Begäraren är Kopia.
