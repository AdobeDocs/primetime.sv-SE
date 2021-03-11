---
title: Översikt över anpassad autentisering/tillstånd (valfritt)
description: Översikt över anpassad autentisering/tillstånd (valfritt)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Översikt över anpassad autentisering/tillstånd (valfritt){#custom-authentication-entitlement-overview-optional}

Primetime Cloud DRM kan konfigureras att nå ut till din egen back-end-autentisering/berättigandetjänst för att avgöra:

* Får den här användaren hämta en licens?
* Vilka rättigheter/begränsningar ska ingå i licensen?

Primetime Cloud DRM innehåller en referensimplementering av en back-end-autentisering/berättigandetjänst. I demonstrationssyfte utfärdar den här servern&quot;tillåt&quot; svar på BEES-förfrågningar. Se [!DNL BEESServlet.java] om du vill ändra serverfunktionen.

>[!NOTE]
>
>Tidigare var detta en separat produkt som heter *Back End Entitlement Server* (BEES), vilket innebär referenser till BEES i hela det här dokumentet och i källfilerna.

