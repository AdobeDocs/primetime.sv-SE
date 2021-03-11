---
title: Begär ett certifikat (begärande)
description: Begär ett certifikat (begärande)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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
      >Om du vill kopiera CSR-informationen markerar du texten mellan, och inte inkluderar, starttaggen `(-----BEGIN CERTIFICATE REQUEST-----)` och sluttaggen `(-----END CERTIFICATE REQUEST-----)`.

1. Klicka på knappen **[!UICONTROL Submit Request]**.

   Ett e-postmeddelande skickas till kontoadministratören och de sekundära administratörerna för granskning. Begäraren är cc&#39;d.

