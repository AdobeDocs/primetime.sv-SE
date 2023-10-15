---
title: Övervaka Adobe Primetime-autentisering
description: Övervaka Adobe Primetime-autentisering
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Övervaka Adobe Primetime-autentisering {#monitoring-adobe-primetime-authentication}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion {#intro}

Kunder kan använda [Nagios](http://www.nagios.org) eller andra verktyg för att kontrollera om Adobe Primetime-autentisering är aktiverad eller inte.

## Övervaka slutpunkter {#monitoring-endpoints}

### Slutpunkter som du kan övervaka {#endpoints-to-monitor}

* Konfigurationsslutpunkten för alla plattformar: `https://sp.auth.adobe.com/adobe-services/config/[your-config-ID]`- Den är tillgänglig via antingen HTTP eller HTTPS (beroende på vilket val som görs av innehållsleverantörens utvecklare). Om den här slutpunkten saknas betyder det att innehållet inte är tillgängligt på alla plattformar och för alla programmeringsgränssnitten. För det klientlösa REST API:t har vi även följande slutpunkt:  `https://api.auth.adobe.com/adobe-services/config your-config-ID]`.

* Följande slutpunkter ingår i Adobe Primetime-autentiseringswebb-SDK.  Om betal-TV-pass saknas betyder det att betal-TV-pass inte används för alla programmerare och alla webbegenskaper:

   * `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js`
   * `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`


### Slutpunkter som du inte bör övervaka {#endpoints-not-monitor}

* `https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer`

  Du får alltid ett 503-fel eftersom den här slutpunkten behöver ett MVPD SAML-svar på den.

* Andra berättigandeslutpunkter - `adobe-services/1.0/authenticate/`, `adobe-services/1.0/deviceShortAuthorize`, `adobe-services/1.0/authorize`

Du kan inte övervaka de här slutpunkterna eftersom de behöver en nyttolast för ett relevant svar.