---
title: REST API-referens
description: Rest api reference
exl-id: 67e4639e-db0b-4400-bb81-e214263e8395
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 4%

---

# REST API-referens {#rest-api-reference}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Svarsformat {#response-formats}


>[!NOTE]
>
> De API:er som tillhandahålls i dessa tjänster kan returnera svar i antingen XML eller JSON (för API:er som returnerar ett svar). Det finns tre olika sätt att ange svarsformatet i begäran:
>
>* Ange HTTP Accept Header till `application/xml` eller `application/json`.
>* Ange parametern i nyttolasten för begäran `format=xml` eller `format=json`.
>* Anropa webbtjänstens slutpunkt med tillägg `.xml` eller `.json`. Till exempel: `/regcode.xml` eller `/regcode.json`
>
>Du kan ange en ENDA av ovanstående metoder. Om du anger flera metoder med olika format kan det leda till fel eller oönskade utdata.

## REST API-slutpunkter {#clientless-endpoints}

&lt;reggie_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

&lt;sp_fqdn>:

* Produktion - [api.auth.adobe.com](http://api.auth.adobe.com/)
* Mellanlagring - [api.auth-staging.adobe.com](http://api.auth-staging.adobe.com/)

</br>


## Sammanfattning av webbtjänster {#web_srvs_summary}

Tabellen nedan visar de tillgängliga webbtjänsterna för kundlösa metoder. Klicka på webbtjänstens slutpunkter om du vill ha mer information (exempelbegäran och svar, indataparametrar, HTTP-metoder osv.)


| Sr | Slutpunkt för webbtjänst | Beskrivning | <!--[Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration)-->. | Hosted At | Anropat av |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestId}/regcode](/help/authentication/registration-code-request.md) | Returnerar slumpmässigt genererad registreringskod och inloggningssidans URI | 2 | Adobe  </br>Reg Code Service | Smart enhet |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestId}/regcode/  </br>  {registrationCode}](/help/authentication/return-registration-record.md) | Returnerar registreringskodposten som innehåller registreringskoden UUID, registreringskoden och det hash-kodade enhets-ID:t | 8 | Adobe  </br>Reg Code Service | Primetime-autentisering |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestId}](/help/authentication/provide-mvpd-list.md) | Returnerar en lista över konfigurerade MVPD-filer för den som gjorde begäran | 5 | Adobe  </br>Primetime  </br>autentisering  </br>Tjänst | Inloggning  </br>Webb  </br>App |
| 4. | [&lt;sp_fqdn>/api/v1/authenticate](/help/authentication/initiate-authentication.md) | Initierar AuthN-processen genom att informera MVPD-markeringshändelsen. Skapar en post i autentiseringsdatabasen som är avstämd när ett godkänt svar tas emot från MVPD (steg 13) | 7 | Adobe  </br>Primetime  </br>autentisering  </br>Tjänst | Inloggning  </br>Webb  </br>App |
| 5. | SAML Assertion Consumer | Befintligt SAML-arbetsflöde mellan Primetime-autentisering och MVPD | 13 | Primetime  </br>autentisering  </br>Tjänst | Primetime-autentisering |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](/help/authentication/check-authentication-flow-by-second-screen-web-app.md) | Inloggningswebbappen kan kontrollera om inloggningsflödet lyckades |  | Primetime  </br>autentisering   </br>Tjänst | Inloggning   </br>Webb   </br>App |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | Hämtar AuthN-tokenrelaterade metadata | 15 | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestId}/regcode/  </br>  {registrationCode}](/help/authentication/delete-registration-record.md) | Tar bort reg.kodposten och släpper reg.koden för återanvändning | 16 | Adobe  </br>Reg Code Service | Primetime-autentisering |
| 9. | [&lt;sp_fqdn>/api/v1/authorized](/help/authentication/initiate-authorization.md) | Hämtar auktoriseringssvar. | 17 | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](/help/authentication/check-authentication-token.md) | Anger om enheten har en AuthN-token som inte har gått ut. |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md) | Returnerar AuthN-token om den hittas. |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](/help/authentication/retrieve-authorization-token.md) | Returnerar AuthZ-token om den hittas. |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](/help/authentication/obtain-short-media-token.md) | Returnerar Short Media Token om den hittas - samma som /api/v1/mediatoken |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](/help/authentication/obtain-short-media-token.md) | Hämtar kort mediatoken |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 15. | [&lt;sp_fqdn>/api/v1/preauthorized](/help/authentication/retrieve-list-of-preauthorized-resources.md) | Hämtar listan över förauktoriserade resurser |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 16. | [&lt;sp_fqdn>/api/v1/preAuthze/{code}](/help/authentication/retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md) | Hämtar listan över förauktoriserade resurser |  | Primetime  </br>autentisering  </br>Tjänst | Inloggningswebbapp |
| 17. | [&lt;sp_fqdn>/api/v1/utloggning](/help/authentication/initiate-logout.md) | Ta bort AuthN- och AuthZ-tokens från lagring |  | Primetime  </br>autentisering   </br>Tjänst | Smart enhet |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](/help/authentication/user-metadata.md) | Hämtar användarmetadata när autentiseringsflödet har slutförts | Ej tillämpligt | Ej tillämpligt | Smart enhet |
| 19. | [&lt;sp_fqdn>/api/v1/authenticate/freepreview](/help/authentication/free-preview-for-temp-pass-and-promotional-temp-pass.md) | Skapa en autentiseringstoken för tillfälligt pass eller tillfälligt kampanjpass | Ej tillämpligt | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |


## REST API-säkerhet {#security}

Alla klientlösa API:er för Primetime-autentisering måste anropas med HTTPS-protokollet för säker kommunikation. Dessutom bör de flesta API:er som anropas innehålla en åtkomsttoken som tillhandahålls av [Dynamisk klientregistrering](/help/authentication/dynamic-client-registration.md).
