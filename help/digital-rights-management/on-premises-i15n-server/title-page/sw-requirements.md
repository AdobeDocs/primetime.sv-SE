---
description: 'null'
seo-description: 'null'
seo-title: Programvarukrav
title: Programvarukrav
uuid: 9faa229b-1abf-4b55-b293-247777bcb1db
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

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
* [!DNL ROOT] - innehåller en [!DNL crossdomain.xml] fil

* ECI-cachefiler - förnedladdade
* [!DNL addIndivCert.py] - Ett skript som uppdaterar en licensservers pålitlighetsrot för att stödja On Premises-personaliseringar
* [!DNL CreateMetadata.jar] - Ett verktyg för att skapa DRM-metadata på plats
* [!DNL client_sample/] - En mapp med ett klientkodfragment
* Versionsinformation - För eventuella sista minuten-tillägg till dokumentationen

## Hämta certifikat för enskilda servrar{#obtain-individualization-server-certificates}

Om du vill använda On Premises Individualization Server måste du först skaffa två digitala autentiseringsuppgifter (certifikat):

* *Autentiseringsuppgifter* för Individualization Transport - utfärdat av Adobe
* *Autentiseringsuppgifter* för individuellt certifikatutfärdare - utfärdad av Symantec (VeriSign)

För att få dessa certifikat skickar du en begäran via Zendesk-biljett till: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Observera att dessa autentiseringsuppgifter är utöver de autentiseringsuppgifter som krävs för att köra en Primetime DRM-licensserver.