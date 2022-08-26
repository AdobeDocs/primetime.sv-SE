---
title: Hämta plattformens SSO-profilbegäran
description: Hämta plattformens SSO-profilbegäran
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Hämta plattformens SSO-profilbegäran {#retrieve-platform-sso-profile-request}

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

Den här resursen skapar profilförfrågningar för begärande-ID och MVPD-tuppel.


| Slutpunkt | Anropat  </br>Av | Indata   </br>Parametrar | HTTP  </br>Metod | Svar | HTTP  </br>Svar |
| --- | --- | --- | --- | --- | --- |
| &lt;sp_fqdn>/api/v1/{beställare}/profile-requests/{mvpd} | Strömmande app</br></br>eller</br></br>Programmerartjänst | 1. begärande (path param)</br>2. mvpd (path param)</br>3. deviceType (obligatoriskt) | GET | Svarets Content-Type blir application/octet-stream eftersom den faktiska nyttolasten är ogenomskinlig för klientprogrammet.</br></br>Svaret bör vidarebefordras av programmet till plattformen</br></br>SSO-motor för att erhålla en profil-SSO. | 200 - lyckades   </br>400 - Ogiltig begäran |


| Indataparameter | Beskrivning |
| --------------- | -------------------------------------------------------------------------------------------------------- |
| begärande | Programmerarens requestId som den här åtgärden är giltig för. |
| mvpd | Det MVPD-ID som den här åtgärden är giltig för. |
| deviceType | Den Apple-plattform som vi försöker få en profilbegäran för.  Antingen **iOS** eller **tvOS**. |

### [Tillbaka till REST API-referens](http://tve.helpdocsonline.com/rest-api-reference)
