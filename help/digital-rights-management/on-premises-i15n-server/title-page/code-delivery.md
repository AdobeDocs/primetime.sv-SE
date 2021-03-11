---
title: Kodleverans/paketinnehåll
description: Kodleverans/paketinnehåll
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Kodleverans/paketinnehåll{#code-delivery-package-contents}

Paketet Adobe Primetime DRM On Premises Individualization Server innehåller följande:

* [!DNL flashaccess.war] - Individualiseringsservern
* [!DNL flashaccess-kgs.war] - Nyckelgenereringsservern (tillval)
* [!DNL /shared] - Innehåller:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - Exempel på egenskapsfil

* [!DNL thirdparty/] - Inkluderar stöd för Crypto-J som systemspecifika bibliotek:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Ett verktyg för kryptering av serverautentiseringsuppgifter
* [!DNL ROOT] - innehåller en  [!DNL crossdomain.xml] fil

* ECI-cachefiler - förnedladdade
* [!DNL addIndivCert.py] - Ett skript som uppdaterar en licensservers pålitlighetsrot för att stödja On Premises-personaliseringar
* [!DNL CreateMetadata.jar] - Ett verktyg för att skapa DRM-metadata på plats
* [!DNL client_sample/] - En mapp med ett klientkodfragment
* Versionsinformation - För eventuella sista minuten-tillägg till dokumentationen

