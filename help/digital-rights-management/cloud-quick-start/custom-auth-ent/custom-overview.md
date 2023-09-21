---
title: Översikt över anpassad autentisering/tillstånd (valfritt)
description: Översikt över anpassad autentisering/tillstånd (valfritt)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Översikt över anpassad autentisering/tillstånd (valfritt){#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM kan konfigureras att nå ut till din egen back-end-autentisering/berättigandetjänst för att avgöra:

* Får den här användaren hämta en licens?
* Vilka rättigheter/begränsningar ska ingå i licensen?

Primetime Cloud DRM innehåller en referensimplementering av en back-end-autentisering/berättigandetjänst. I demonstrationssyfte utfärdar den här servern&quot;tillåt&quot; svar på BEES-förfrågningar. Se [!DNL BEESServlet.java] för att ändra serverfunktionen.

>[!NOTE]
>
>Tidigare var detta en separat produkt som hette *Server för bakomliggande tillstånd* (BEES), dvs. referenserna till BEES i hela dokumentet och i källfilerna.
