---
seo-title: Begär ett certifikat (begärande)
title: Begär ett certifikat (begärande)
uuid: f0d7f65d-681d-430f-b67b-3bdceb4b6d37
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

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
      >Om du vill kopiera CSR-informationen markerar du texten mellan, och inte inklusive, start- `(-----BEGIN CERTIFICATE REQUEST-----)` och sluttaggen `(-----END CERTIFICATE REQUEST-----)`.

1. Klicka på **[!UICONTROL Submit Request]** knappen.

   Ett e-postmeddelande skickas till kontoadministratören och de sekundära administratörerna för granskning. Begäraren är cc&#39;d.

