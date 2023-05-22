---
title: Översikt över anpassad autentisering/tillstånd (valfritt)
description: Översikt över anpassad autentisering/tillstånd (valfritt)
copied-description: true
exl-id: d92c4246-c772-44da-80b6-4086dfc30ff4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
