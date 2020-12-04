---
seo-title: Översikt över anpassad autentisering/tillstånd (valfritt)
title: Översikt över anpassad autentisering/tillstånd (valfritt)
uuid: 8b5e38a5-562c-4781-ac40-4b3d6cdd97fe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
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

