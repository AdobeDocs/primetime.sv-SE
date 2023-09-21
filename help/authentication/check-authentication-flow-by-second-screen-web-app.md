---
title: Kontrollera autentiseringsflöde med andra skärmens webbapp
description: Kontrollera autentiseringsflöde med andra skärmens webbapp
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Kontrollera autentiseringsflöde med andra skärmens webbapp {#check-authentication-flow-by-second-screen-web-app}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## REST API-slutpunkter {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>

## Beskrivning {#description}

Detta API bör användas av webbprogrammet för inloggning på andra skärmen för att bekräfta att Adobe Primetime-autentisering har bekräftat att inloggningen från MVPD lyckades. Vi rekommenderar att du anropar denna API innan du visar ett meddelande till slutanvändaren som instruerar användaren att fortsätta till enhetskonsolen för att fortsätta med arbetsflödena.


| Slutpunkt | Anropat  </br>Av | Indata   </br>Parametrar | HTTP  </br>Metod | Svar | HTTP  </br>Svar |
| --- | --- | --- | --- | --- | --- |
| SP_FQDN/api/v1/checkauthn/{registreringskod} | Inloggningswebbapp | 1. Registreringskod  </br>    (Bankomponent)</br>2.  begärande  </br>    (Obligatoriskt) | GET | XML eller JSON som innehåller felinformation om det misslyckas. | 200 - lyckades   </br>403 - Ej tillåtet |

</br>

| Indataparameter | Beskrivning |
| ----------------- | --------------------------------------------------------------------------------------------- |
| registreringskod | Registreringskodvärdet som anges av användaren i början av autentiseringsflödet. |
| begärande | Programmerarens requestId som den här åtgärden är giltig för. |


### Exempelsvar (vid fel) {#response}

```JSON
    {
        "status": 403,
        "message": "Forbidden"
    }
```

### [Tillbaka till REST API-referens](/help/authentication/rest-api-reference.md)
