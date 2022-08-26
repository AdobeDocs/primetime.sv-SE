---
title: REST API-referens
description: Rest api reference
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 3%

---


# REST API-referens {#rest-api-reference}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Svarsformat {#response-formats}


>[!NOTE]
>
> De API:er som tillhandahålls i dessa tjänster kan returnera svar i antingen XML eller JSON (för API:er som returnerar ett svar). Det finns tre olika sätt att ange svarsformatet i begäran:
>* Ange HTTP Accept Header till &quot;application/xml</code>&quot; eller &quot;application/json</code>&quot;
>* Ange parametern &quot;format=xml&quot; i nyttolasten för begäran</code>&quot; eller &quot;format=json</code>&quot;</li>
>* Anropa webbtjänstens slutpunkt med filtillägget .xml</code> eller .json</code>. Till exempel&quot;/regcode.xml</code>&quot; eller &quot;/regcode.json</code>&quot;
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


| Sr | Slutpunkt för webbtjänst | Beskrivning | [Diag.  </br>Ref](http://tve.helpdocsonline.com/api-reference-v2-test#illustration). | Hosted At | Anropat av |
| --- | --- | --- | --- | --- | --- |
| 1. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestId}/regcode](http://tve.helpdocsonline.com/registration-code-request) | Returnerar slumpmässigt genererad registreringskod och inloggningssidans URI | 2 | Adobe  </br>Reg Code Service | Smart enhet |
| 2. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/return-registration-record) | Returnerar registreringskodposten som innehåller registreringskoden UUID, registreringskoden och det hash-kodade enhets-ID:t | 8 | Adobe  </br>Reg Code Service | Primetime-autentisering |
| 3. | [&lt;sp_fqdn>/api/v1/config/  </br>  {requestId}](http://tve.helpdocsonline.com/provide-mvpd-list) | Returnerar en lista över konfigurerade MVPD-filer för den som gjorde begäran | 5 | Adobe  </br>Primetime  </br>autentisering  </br>Tjänst | Inloggning  </br>Webb  </br>App |
| 4. | [&lt;sp_fqdn>/api/v1/authenticate](http://tve.helpdocsonline.com/initiate-authentication) | Initierar AuthN-processen genom att informera MVPD-markeringshändelsen. Skapar en post i autentiseringsdatabasen som är avstämd när ett godkänt svar tas emot från MVPD (steg 13) | 7 | Adobe  </br>Primetime  </br>autentisering  </br>Tjänst | Inloggning  </br>Webb  </br>App |
| 5. | SAML Assertion Consumer | Befintligt SAML-arbetsflöde mellan Primetime-autentisering och MVPD | 13 | Primetime  </br>autentisering  </br>Tjänst | Primetime-autentisering |
| 6. | [&lt;sp_fqdn>/api/v1/checkauthn/  </br>  {registrationCode}](http://tve.helpdocsonline.com/check-authentication-flow-by-second-screen-web-app) | Inloggningswebbappen kan kontrollera om inloggningsflödet lyckades |  | Primetime  </br>autentisering   </br>Tjänst | Inloggning   </br>Webb   </br>App |
| 7. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | Hämtar AuthN-tokenrelaterade metadata | 15 | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 8. | [&lt;reggie_fqdn>/reggie/v1/  </br>  {requestId}/regcode/  </br>  {registrationCode}](http://tve.helpdocsonline.com/delete-registration-record) | Tar bort reg.kodposten och släpper reg.koden för återanvändning | 16 | Adobe  </br>Reg Code Service | Primetime-autentisering |
| 9. | [&lt;sp_fqdn>/api/v1/authorized](http://tve.helpdocsonline.com/initiate-authorization) | Hämtar auktoriseringssvar. | 17 | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 10. | [&lt;sp_fqdn>/api/v1/checkauthn](http://tve.helpdocsonline.com/check-authentication-token) | Anger om enheten har en AuthN-token som inte har gått ut. |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 11. | [&lt;sp_fqdn>/api/v1/tokens/authn](http://tve.helpdocsonline.com/rest-api-retrieve-authentication-token) | Returnerar AuthN-token om den hittas. |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 12. | [&lt;sp_fqdn>/api/v1/tokens/authz](http://tve.helpdocsonline.com/retrieve-authorization-token) | Returnerar AuthZ-token om den hittas. |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 13. | [&lt;sp_fqdn>/api/v1/tokens/media](http://tve.helpdocsonline.com/obtain-short-media-token) | Returnerar Short Media Token om den hittas - samma som /api/v1/mediatoken |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 14. | [&lt;sp_fqdn>/api/v1/mediatoken](http://tve.helpdocsonline.com/obtain-short-media-token) | Hämtar kort mediatoken |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 15. | [&lt;sp_fqdn>/api/v1/preauthorized](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources) | Hämtar listan över förauktoriserade resurser |  | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |
| 16. | [&lt;sp_fqdn>/api/v1/preAuthze/{code}](http://tve.helpdocsonline.com/retrieve-list-of-preauthorized-resources-by-way-of-web-app) | Hämtar listan över förauktoriserade resurser |  | Primetime  </br>autentisering  </br>Tjänst | Inloggningswebbapp |
| 17. | [&lt;sp_fqdn>/api/v1/utloggning](http://tve.helpdocsonline.com/logout) | Ta bort AuthN- och AuthZ-tokens från lagring |  | Primetime  </br>autentisering   </br>Tjänst | Smart enhet |
| 18. | [&lt;sp_fqdn>/api/v1/tokens/usermetadata](http://tve.helpdocsonline.com/user-metadata-call) | Hämtar användarmetadata när autentiseringsflödet har slutförts | Ej tillämpligt | Ej tillämpligt | Smart enhet |
| 19. | [&lt;sp_fqdn>/api/v1/authenticate/freepreview](http://tve.helpdocsonline.com/free-preview-for-temp-pass-and-promotional-temp-pass) | Skapa en autentiseringstoken för tillfälligt pass eller tillfälligt kampanjpass | Ej tillämpligt | Primetime  </br>autentisering  </br>Tjänst | Smart enhet |

{style=&quot;table-layout:auto&quot;}

## REST API-säkerhet {#security}

Alla klientlösa API:er för Primetime-autentisering måste anropas med HTTPS-protokollet för säker kommunikation. Dessutom bör de flesta API:er som anropas innehålla en åtkomsttoken som tillhandahålls av [Dynamisk klientregistrering](http://tve.helpdocsonline.com/dynamic-client-registration).


## Relaterad information {#related}

* [REST API - översikt](http://tve.helpdocsonline.com/reset-api-overview)
* [Server-till-server-kokbok](http://tve.helpdocsonline.com/server-to-server-cookbook)
* [Klient-till-server-kokbok](http://tve.helpdocsonline.com/client-to-server)
* [Undvik att använda &#39;&amp;&#39;reg\_code i /authenticate request (Tech Note)](https://tve.zendesk.com/entries/23648011-Clientless-Avoid-using-reg-code-in-authenticate-request)
