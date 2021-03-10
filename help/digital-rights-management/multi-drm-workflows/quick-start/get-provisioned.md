---
description: För att komma igång med Primetime DRM Cloud, som drivs av ExpressPlay, måste du konfigurera Adobe Cert- och ExpressPlay-konton med din Adobe-representant.
title: Skaffa licenser (konton, etc.)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---


# Få etablerat (konton osv.) {#get-provisioned-accounts-etc}

För att komma igång med Primetime DRM Cloud, som drivs av ExpressPlay, måste du konfigurera Adobe Cert- och ExpressPlay-konton med din Adobe-representant.

1. Kontakta din Adobe-representant och begär de Adobe Cert- och ExpressPlay-konton du behöver för att implementera Multi-DRM med TVSDK.

       Ange den e-postadress som du vill använda som kontaktpunkt för din Adobe-representant. Adobe skapar sedan två konton åt dig:
   
   * ***Certifikatportalkonto***  - (<span></span>https://certportal.primetime.adobe.com): DRM- *certifikatregistreringsteamet för DRM-certifikat/Primetime* Adobe Access/Primetime skickar ett e-postmeddelande till de adresser du har angett. E-postmeddelandet innehåller URL:en för Adobe cert-portalen, tillsammans med en länk till dokumentationen för registrering av Adobe-certifikat (de senaste dokumenten finns här: [Handbok för certifikatregistrering](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md)).

   * ***ExpressPlay-konto***  - Adobe skickar ett e-postmeddelande till dig som innehåller en länk som du använder för att registrera ditt ExpressPlay-administratörskonto.

1. Logga in på Adobe certifikatportal med din Adobe ID (använd samma e-postadress som du angav för Adobe). Om du inte har någon Adobe ID ännu kan du snabbt skapa en genom att följa länken *Hämta en Adobe ID* från certifikatportalen:

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. Begär ett *test*-certifikat på Adobe certifikatportal.

   För Multi-DRM-testversionen kommer ett och samma testcertifikat att omfatta alla dessa aspekter av innehållsskydd: paketering, licensiering och transport. Du måste ange din egen [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) för att kunna begära ett certifikat:
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe kommer att skicka ett e-postmeddelande till dig som anger att du godkänner eller avvisar din certifikatbegäran. Du kan se status för dina certifikatbegäranden på fliken *Begäranhistorik* på certifikatportalen:
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. Skapa ett ExpressPlay-administratörskonto.

   Följ länken till ExpressPlay som Adobe har gett dig. Sidan *Skapa ett konto* öppnas på ExpressPlay. Fyll i de obligatoriska uppgifterna och skicka in formuläret. Du får ett e-postmeddelande från `operations@expressplay.com` med en aktiveringslänk som är bra i en vecka. Konfigurera ExpressPlay-tjänsten när du har aktiverat:
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   När du har skapat tjänsten visas din egen Admin-sida. Tillsammans med vissa aktivitetsspårningsfält kan du visa dina produktions- och testautentiserare *kundautentiserare* (API-nycklar) och dina produktions- och testtjänste-URL:er:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. Om du använder FairPlay krävs ytterligare steg (på Apples utvecklingswebbplats) för att komma igång med ExpressPlay. Mer information finns i [Aktivera ExpressPlay-tjänsten för FairPlay](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay).
