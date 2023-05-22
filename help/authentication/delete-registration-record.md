---
title: Ta bort registreringspost
description: Ta bort registreringspost
exl-id: 42707070-2e1f-4847-93fd-30025aef56c1
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Ta bort registreringspost {#delete-registration-record}

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


## Beskrivning {#delete-record}

Tar bort reg.kodposten och släpper reg.koden för återanvändning. 

| Slutpunkt | Anropat  </br>Av | Indata   </br>Parametrar | HTTP  </br>Metod | Svar | HTTP  </br>Svar |
| --- | --- | --- | --- | --- | --- |
| &lt;reggie_fqdn>/reggie/v1/{requestId}/regcode/{registrationCode}</br></br>Till exempel:</br></br>&lt;reggie_fqdn>/reggie/v1/regcode/ER45RTY | Strömmande app</br></br>eller</br></br>Programmerartjänst | 1. Begärande-ID  </br>    (Bankomponent)</br>2.  Registreringskod  </br>    (Bankomponent) | DELETE | Ingen | 204 |

{style="table-layout:auto"}

</br>

| Indataparameter | Beskrivning |
| --- | --- |
| begärande | Programmerarens requestId som den här åtgärden är giltig för. |
| registreringskod | Registreringskodvärdet som skulle visas på direktuppspelningsenheten (anges i autentiseringsflödet). |

{style="table-layout:auto"}

</br>

### [Tillbaka till REST API-referens](/help/authentication/rest-api-reference.md)
