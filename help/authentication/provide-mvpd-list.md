---
title: Ange MVPD-lista
description: Ange MVPD-lista
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Ange MVPD-lista {#provide-mvpd-list}

## REST API-slutpunkter {#clientless-endpoints}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

&lt;reggie_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

 </br>

## Beskrivning {#description}

Returnerar en lista över konfigurerade MVPD-filer för den som gjorde begäran.

| Slutpunkt | Anropat  </br>Av | Indata   </br>Parametrar | HTTP  </br>Metod | Svar | HTTP  </br>Svar |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/config/{requestedId}</br></br>Till exempel:</br></br>&lt;sp_fqdn>/api/v1/config/sampleRequestorId | Primetime-autentisering | 1. Begärande</br>    (Bankomponent)</br>_2.  deviceType (utgått)_ | GET | XML eller JSON som innehåller en lista över PDF-filer. | 200 |

{style=&quot;table-layout:auto&quot;}


| Indataparameter | Beskrivning |
| --------------- | ------------------------------------------------------------- |
| begärande | Programmerarens requestId som den här åtgärden är giltig för. |
| *deviceType* | Enhetstyp. |

{style=&quot;table-layout:auto&quot;}

### Exempelsvar {#sample-response}

Samma som det befintliga MVPD XML-svaret till /config-servern

Obs! Alla MVPD-program som är konfigurerade att använda enkel inloggning (Platform SSO) har följande extra egenskaper i motsvarande nod (JSON/XML):

* **enablePlatformServices (boolean):** flagga som anger om denna MVPD är integrerad via plattformens SSO
* **boardingStatus (sträng):** flagga som anger om MVPD har fullt stöd för Platform SSO (SUPPORTED) eller om MVPD bara visas i plattformsväljaren (PICKER)
* **displayInPlatformPicker (boolean):** om det här videofilmsprogrammet ska visas i plattformsväljaren
* **platformMappingId (sträng):** identifieraren för detta MVPD så som den är känd av plattformen
* **requiredMetadataFields (strängmatris):** de metadatafält för användaren som förväntas vara tillgängliga vid en lyckad inloggning


[Tillbaka till API-referens utan klient](http://tve.helpdocsonline.com/clientless-api-reference)
