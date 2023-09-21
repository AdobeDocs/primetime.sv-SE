---
title: Programvarukrav
description: Programvarukrav
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Programvarukrav {#software-requirements}

* Tomcat 6
* JDK 1.8

## Kodleverans/paketinnehåll{#code-delivery-package-contents}

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
* [!DNL ROOT] - innehåller [!DNL crossdomain.xml] fil

* ECI-cachefiler - förnedladdade
* [!DNL addIndivCert.py] - Ett skript som uppdaterar en licensservers pålitlighetsrot för att stödja On Premises-personaliseringar
* [!DNL CreateMetadata.jar] - Ett verktyg för att skapa DRM-metadata på plats
* [!DNL client_sample/] - En mapp med ett klientkodfragment
* Versionsinformation - För eventuella sista minuten-tillägg till dokumentationen

## Hämta certifikat för enskilda servrar{#obtain-individualization-server-certificates}

Om du vill använda On Premises Individualization Server måste du först skaffa två digitala autentiseringsuppgifter (certifikat):

* *Autentiseringsuppgifter för Individuell transport* - utfärdat av Adobe
* *Autentiseringsuppgifter för Individuell certifikatutfärdare* - utfärdat av Symantec (VeriSign)

För att få dessa certifikat skickar du en begäran via Zendesk-biljett till: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Observera att dessa autentiseringsuppgifter är utöver de autentiseringsuppgifter som krävs för att köra en Primetime DRM-licensserver.
