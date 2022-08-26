---
title: Kostnadsfri förhandsgranskning för tillfälligt pass och tillfälligt kampanjpass
description: Kostnadsfri förhandsgranskning för tillfälligt pass och tillfälligt kampanjpass
source-git-commit: 0839e9f2eac7eeeadf9bbfafb2bdd76596f4fb06
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 1%

---


# Kostnadsfri förhandsgranskning för tillfälligt pass och tillfälligt kampanjpass {#free-preview-for-temp-pass-and-promotional-temp-pass}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## REST API-slutpunkter {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Beskrivning {#description}

Tillåter att en autentiseringstoken skapas för tillfälligt pass- och kampanjtillfälligt pass utan behov av en andra skärm.


| Slutpunkt | Anropat  </br>Av | Indata   </br>Parametrar | HTTP  </br>Metod | Svar | HTTP  </br>Svar |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/authenticate/freepreview | Strömmande app</br></br>eller</br></br>Programmerartjänst | 1. request_id (obligatoriskt)</br>    </br>2.  deviceId (obligatoriskt)</br>    </br>3.  mso_id (obligatoriskt)</br>    </br>4.  domain_name (obligatoriskt)</br>    </br>5.  device_info/X-Device-Info (obligatoriskt)</br>6.  deviceType</br>    </br>7.  deviceUser (utgått)</br>    </br>8.  appId (utgått)</br>    </br>9.  generisk_data (valfritt) | POST | Svaret blir 2004 No Content, vilket anger att token har skapats och är klar att användas för redigeringsflödena. | 204 - Inget innehåll   </br>400 - Ogiltig begäran |

<div>


| Indataparameter | Beskrivning |
| --- | --- |
| beställare_id | Programmerarens requestId som den här åtgärden är giltig för. |
| deviceId | Byte för enhets-ID. |
| mso_id | Det MVPD-ID som den här åtgärden är giltig för. |
| domain_name | Domännamnet som en token ska beviljas för. Detta jämförs med domänerna för tjänsteleverantören när en auktoriseringstoken beviljas. |
| device_info/</br></br>X-Device-Info | Information om direktuppspelningsenhet.</br></br>**Anteckning**: Detta kan skickas som en URL-parameter för device_info, men på grund av parameterns potentiella storlek och begränsningar i längden på en GET-URL bör det skickas som X-Device-Info i http-huvudet. </br></br>Läs mer här: [Skicka information om enhet och anslutning](http://tve.helpdocsonline.com/passing-device-information). |
| _deviceType_ | Enhetstypen (t.ex. Roku, PC).</br></br>Om den här parametern är korrekt angiven erbjuder ESM värden som är [uppdelad per enhetstyp](http://tve.helpdocsonline.com/esm-overview$clientless_device_type) när du använder Klientlös, så att olika typer av analyser kan utföras för t.ex. Roku, AppleTV, Xbox osv.</br></br>http://tve.helpdocsonline.com/clientless-device-type-benefits-on-pass-metrics </br></br>**Anteckning**: device_info ersätter den här parametern. |
| _deviceUser_ | Enhetens användaridentifierare.</br></br>**Anteckning**: Om det används ska deviceUser ha samma värden som i [Skapa registreringskod](http://tve.helpdocsonline.com/registration-code-request) begäran. |
| _appId_ | Program-ID/namn. </br></br>**Anteckning**: device_info ersätter den här parametern. Om den används, `appId` ska ha samma värden som i [Skapa registreringskod](http://tve.helpdocsonline.com/create-registration-page-/-login-uri) begäran. |
| generisk_data | Används för att begränsa omfattningen av token för tillfälligt kampanjpass. |


### [Tillbaka till REST API-referens](http://tve.helpdocsonline.com/rest-api-reference)
