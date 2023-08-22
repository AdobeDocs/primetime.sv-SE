---
title: Förbättrade felkoder
description: Förbättrade felkoder
exl-id: 2b0a9095-206b-4dc7-ab9e-e34abf4d359c
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# Förbättrade felkoder {#enhanced-error-codes}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Ökning {#overview}

I det här dokumentet beskrivs en lista över API-felkoder och ytterligare felinformation som returneras till programmen.

Om du vill använda Enhanced Error Codes i programmerarprogrammet måste en begäran göras till supportteamet för att det ska kunna aktiveras med en konfigurationsändring.

## Hantering av svarsfel {#response-error-handling}

I de flesta fall innehåller Primetimes autentiserings-API ytterligare felinformation i svarstexten för att kunna tillhandahålla **kontext** om varför ett visst fel har inträffat och/eller möjliga lösningar på problemet automatiskt.  *I vissa specifika fall som omfattar autentiserings- eller utloggningsflöden kan dock Primetimes autentiseringstjänster returnera ett HTML-svar eller en tom brödtext. Mer information finns i API-dokumentationen.*

Även om vissa typer av fel kan hanteras automatiskt (till exempel att försöka göra om en auktoriseringsbegäran i händelse av en timeout i nätverket eller kräva att användaren autentiserar sig om sessionen har gått ut), kan andra typer kräva konfigurationsändringar eller att kundtjänstgruppen interagerar. Det är viktigt för programmerare att samla in och lämna fullständig felinformation i sådana fall.

Primetimes autentiserings-API returnerar HTTP-statuskoder i intervallet 400-500 för att ange fel eller fel. Varje HTTP-statuskod har vissa konsekvenser:

- De 4xx-felkoderna innebär att felet genereras av klienten och att klienten måste utföra ytterligare arbete för att åtgärda det (t.ex. hämta en åtkomsttoken innan skyddade API:er anropas eller tillhandahålla en obligatorisk parameter)

- Felkoderna 5xx innebär att felet genereras av servern och att servern måste utföra ytterligare arbete för att åtgärda det.

Ytterligare felinformation finns i felfältet i svarstexten.




| Namn | Typ | Exempel | Beskrivning |
| --- | --- | --- | --- |
| **fel** | _object_ | JSON <br>    {<br>        &quot;status&quot; : 403,<br>        &quot;code&quot; : &quot;network_connection_error&quot;,<br>        &quot;message&quot; :&quot;Det går inte att kontakta din TV-leverantör&quot;,<br>        &quot;helpUrl&quot; : &quot;&quot;,<br>        &quot;trace&quot; : &quot;12f6fef9-d2e0-422b-a9d7-60d799abe353&quot;,<br>        &quot;action&quot; : &quot;retry&quot;<br>    }<br><br>—<br><br>XML<br><br>`<``error``>`<br><br>`<``status``>403</``status``>`<br><br>`<``code``>network_connection_failure</``code``>`<br><br>`<``message``>Unable to contact your TV provider services</``message``>   <``helpUrl``></``helpUrl``>`<br><br>`<``trace``>12f6fef9-d2e0-422b-a9d7-60d799abe353</``trace``>`<br><br>`<``action``>retry</``action``>`<br><br>`</``error``> ` | En samling eller felobjekt som samlats in när begäran skulle slutföras. |

</br>

Adobe Primetime-API:er som hanterar flera objekt (API för förhandsauktorisering, etc.) kan visa om bearbetningen misslyckades för ett visst objekt och lyckades för andra objekt med hjälp av felinformation på objektnivå. I det här fallet ***&quot;error&quot;*** objektet finns på objektnivå och svarstexten kan innehålla flera ***&quot;errors&quot;*** -objekt - se API-dokumentationen.

</br>

| Exempel med partiell framgång och fel på objektnivå |
| ---------------------- |
| <pre lang="json">JSON <br>{<br>  &quot;id&quot; : &quot;TestStream1&quot;,<br>  &quot;authorized&quot; : true <br>}, </br>{ </br>  &quot;id&quot; : &quot;TestStream2&quot;, <br>   &quot;authorized&quot; : false, </br>   &quot;error&quot; : { <br> </br>      &quot;status&quot; : 403,<br>      &quot;code&quot; : &quot;network_connection_error&quot;,<br>      &quot;message&quot; :&quot;Det går inte att kontakta din TV-leverantör&quot;,<br>      &quot;details&quot; : &quot;&quot;,<br>      &quot;helpUrl&quot; : &quot;&quot;,<br>      &quot;trace&quot; : &quot;8bcb17f9-b172-47d2-86d9-3eb146eba85e&quot;,<br>      &quot;action&quot; : &quot;retry&quot;</br>    }<br> </br>   }<br> ] </br>} </pre> |

</br>

Varje felobjekt har följande parametrar:

| Namn | Typ | Exempel | Begränsad | Beskrivning |
|----|----|----|----|--------------|
| Status | *heltal* | 403 | ♦ | HTTP-svarskoden enligt RFC 7231 (https://tools.ietf.org/html/rfc7231#section-6) <br> - 400 Ogiltig begäran <br> - 400 Ogiltig begäran <br> - 400 Ogiltig begäran <br> - 401 Obehörig <br> - 403 Ej tillåtet <br> - 404 Hittades inte <br> - 405 Metoden tillåts inte <br> - 409 Konflikt <br> - 410 borta <br> - 412 Förhandsvillkor misslyckades <br> - 429 För många begäranden <br> - Serverfel för 500 intervall <br> - 503 Tjänsten är inte tillgänglig |
| Code | *string* | network_connection_error | ♦ | Standardfelkoden för Primetime-autentisering. En fullständig lista över felkoder finns nedan. |
| message | *string* | Det går inte att kontakta din TV-leverantör | | Handledsligt läsbart meddelande som kan visas för slutanvändaren. |
| information | *string* | Prenumerationspaketet innehåller inte &quot;Live&quot;-kanalen | | I vissa fall ges ett detaljerat meddelande från slutpunkterna för MVPD-godkännande eller via programmeraren via nedbrytningsregler. <br> <br> Observera att om inget anpassat meddelande togs emot från partnertjänsterna kanske det här fältet inte finns i felfälten. |
| helpUrl | *url* | &quot;&quot; | | En URL som länkar till mer information om varför felet uppstod och möjliga lösningar. <br> <br>  URI:n representerar en absolut URL och bör inte härledas från felkoden. Beroende på felkontexten kan en annan URL anges. Samma felkod för bad_request ger till exempel olika URL:er för autentisering och auktoriseringstjänster. |
| trace | *string* | 12f6fef9-d2e0-422b-a9d7-60d799abe353 | | En unik identifierare för det här svaret som kan användas när support kontaktas för att identifiera specifika problem i mer komplexa scenarier. |
| åtgärd | *string* | försök igen | ♦ | *Rekommenderade åtgärder för att åtgärda situationen:* </br><br> -none - Tyvärr finns det ingen fördefinierad åtgärd för att åtgärda problemet. Detta kan tyda på ett felaktigt anrop av det offentliga API:t </br><br>-configuration - En konfigurationsändring krävs via TVE-instrumentpanelen eller genom att kontakta support. </br><br>-application-registration - Programmet måste registrera sig igen. </br><br>-authentication - Användaren måste autentisera eller autentisera igen. </br><br>-authentication - Användaren måste erhålla auktorisering för den specifika resursen. </br><br>-nedbrytning - någon form av nedbrytning bör appliceras. </br><br>-retry - Ett nytt försök att utföra begäran kan lösa problemet</br><br>-retry-after - Ett nytt försök att utföra begäran efter den angivna tidsperioden kan lösa problemet. |

</br>

**Anteckningar:**

- ***Begränsad*** kolumn *anger om respektive fältvärde representerar en begränsad uppsättning* (t.ex. befintliga HTTP-statuskoder för &quot;*status*&quot; fält). Framtida uppdateringar av den här specifikationen kan lägga till värden i den begränsade listan, men befintliga värden tas inte bort eller ändras. Obegränsade fält kan vanligtvis innehålla alla data, men det kan finnas begränsningar för att säkerställa en rimlig storlek.

- Varje svar från Adobe kommer att innehålla ett&quot;Adobe-Request-Id&quot; som identifierar klientbegäran via våra HTTP-tjänster. The &quot;**trace**&quot; kompletteras av det och de ska rapporteras tillsammans.

## HTTP-statuskoder och felkoder {#http-status-codes-and-error-codes}

Inkonsekvenser mellan olika felkoder och deras associerade HTTP-statuskoder beror på bakåtkompatibilitetskraven med äldre sdks och program (till exempel *unknown\_application* ger 400 felaktiga begäranden under *unknown\_software\_statement* ger 401 otillåtet). Lösningen på dessa inkonsekvenser kommer att riktas in i framtida iterationer.

## Åtgärder och felkoder {#actions-and-error-codes}

För de flesta felkoder kan flera åtgärder vara möjliga som sökvägar för att åtgärda problemet eller till och med flera åtgärder kan behövas för att de ska kunna åtgärdas automatiskt. Vi valde att ange den med störst sannolikhet att åtgärda felet. The **funktionsmakron** kan delas upp i tre kategorier:

1. som försöker åtgärda begärandekontexten (försök igen, försök igen)
1. som försöker åtgärda användarkontexten i programmet (programregistrering, autentisering, auktorisering)
1. som försöker åtgärda integreringssammanhanget mellan ett program och en identitetsleverantör (konfiguration, nedgradering)

För den första kategorin (försök igen och försök igen efter) kan det räcka att försöka utföra samma begäran igen för att lösa problemet. Om API:er hanterar flera objekt, bör programmet upprepa begäran och endast inkludera de objekt som innehåller åtgärden&quot;försök igen&quot; eller&quot;försök igen&quot;. För &quot;*försök igen efter*&quot; action, a &quot;<u>Försök igen efter</u>&quot;header anger hur många sekunder programmet ska vänta innan begäran upprepas.

För den andra och tredje kategorin är den faktiska åtgärdsimplementeringen i hög grad beroende av programfunktionerna. Till exempel &quot;*nedbrytning*&quot; kan implementeras antingen som &quot;växla till 15 minuters temporära pass för att tillåta användare att spela upp innehållet&quot; eller antingen som &quot;automatiskt verktyg för att tillämpa FÖRSTÖRNINGEN AUTHN-ALL eller AUTHZ-ALL för integrering med det angivna MVPD&quot;. Liknande en &quot;*autentisering*&quot; kan utlösa en passiv autentisering (bakåtkanalsautentisering) på en surfplatta och ett helskärmsautentiseringsflöde på anslutna tv-apparater. Därför valde vi att tillhandahålla fullständiga URL:er med schema och alla parametrar.

## Felkoder {#error-codes}

I tabellen nedan visas möjliga felkoder, associerade meddelanden och möjliga åtgärder.

| Åtgärd | Felkod | HTTP-statuskod | Beskrivning |
|---|---|---|--------------|
| konfiguration | *authentication_deny_by_mvpd* | 403 | MVPD har returnerat ett beslut om att neka när den angivna resursen begärdes. |
|  | *permission_deny_by_parental_controls* | 403 | MVPD har returnerat ett beslut om att neka, på grund av inställningar för föräldrakontroll för den angivna resursen. |
|  | *permission_deny_by_programmmer* | 403 | Försämringsregeln som tillämpas av Programmeraren verkställer ett beslut om att neka för den aktuella användaren. |
|  | *bad_request* | 400 | API-begäran är ogiltig eller felaktigt utformad. Granska API-dokumentationen för att fastställa kraven för begäran. |
|  | *individualization_service_unavailable* | 503 | Begäran misslyckades eftersom individualiseringstjänsten inte är tillgänglig. |
|  | *internal_error* | 500 | Begäran misslyckades på grund av ett internt serverfel. |
|  | *invalid_client_time* | 400 | Klientdatorns datum/tid/tidszon är inte korrekt inställd. Detta leder troligtvis till autentiserings-/auktoriseringsfel. |
|  | *invalid_custom_scheme* | 400 | Det angivna anpassade schema som används i programregistreringen känns inte igen. Kontrollera TVE-instrumentpanelens konfiguration för att se om det finns korrekta värden för anpassade scheman. |
|  | *invalid_domain* | 400 | Den som gjorde begäran använder en ogiltig domän. Alla domäner som används av ett visst begärande-ID måste vitlistas av Adobe. |
|  | *invalid_header* | 400 | Begäran misslyckades eftersom den innehöll ett ogiltigt huvud. Granska API-dokumentationen för att avgöra vilka huvuden som är giltiga för din begäran och om det finns några begränsningar för deras värde. |
|  | *invalid_http_method* | 405 | HTTP-metoden som är associerad med begäran stöds inte. Granska API-dokumentationen för att fastställa vilka HTTP-metoder som stöds för din begäran. |
|  | *invalid_parameter_value* | 400 | Begäran misslyckades eftersom den innehöll en ogiltig parameter eller ett ogiltigt parametervärde. Granska API-dokumentationen för att avgöra vilka parametrar som är giltiga för din begäran och om det finns några begränsningar för deras värde. |
|  | *invalid_resource_value* | 400 | Begäran misslyckades eftersom en ogiltig eller felformaterad resurs användes. Granska API-dokumentationen för att avgöra hur komplexa resurser måste kodas för din begäran och om det finns några begränsningar för deras värde och/eller storlek. |
|  | *invalid_registration_code | 404 | Den angivna registreringskoden är inte längre giltig eller har gått ut. |
|  | *invalid_service_configuration* | 500 | Begäran misslyckades på grund av felaktig tjänstkonfiguration. |
|  | *missing_authentication_header* | 400 | Begäran misslyckades eftersom den inte innehåller det autentiseringshuvud som krävs för det specifika API:t. |
|  | *missing_resource_mapping* | 400 | Det finns ingen motsvarande mappning för den angivna resursen. Kontakta supporten för att åtgärda den nödvändiga mappningen. |
|  | *preauthentication_deny_by_mvpd* | 403 | MVPD har returnerat ett beslut om att neka vid begäran om förauktorisering för den angivna resursen. |
|  | *preauthentication_deny_by_programmmer* | 403 | De nedbrytningsregler som tillämpas av programmeraren tillämpar ett beslut om att neka för den aktuella användaren. |
|  | *registration_code_service_unavailable* | 503 | Begäran misslyckades eftersom registreringskodstjänsten inte är tillgänglig. |
|  | *service_unavailable | 503 | Begäran misslyckades på grund av att autentisering eller behörighetskontroll inte är tillgängligt. |
|  | *access_token_unavailable* | 400 | Begäran misslyckades på grund av ett oväntat fel när åtkomsttoken hämtades. Kontrollera konfigurationen av TVE-kontrollpanelen för tillgängliga programsatser och registrerade anpassade scheman. |
|  | *unsupported_client_version* | 400 | Den här versionen av Primetime Authentication SDK är för gammal och stöds inte längre. Läs i API-dokumentationen vad som krävs för att uppgradera till den senaste versionen. |
|  | *network_required_ssl* | 403 | Det finns ett SSL-anslutningsproblem för målpartnertjänsten. Kontakta supportteam. |
|  | *för_många_resurser* | 403 | Begäran om auktorisering eller förauktorisering misslyckades eftersom för många resurser efterfrågades. Kontakta supportteamet för att konfigurera begränsningarna för auktorisering och förhandsauktorisering. |
|  | *unknown_programmmer | 400 | Programmeraren eller tjänsteleverantören känns inte igen. Använd TVE Dashboard för att registrera angiven programmerare. |
|  | *unknown_application* | 400 | Programmet känns inte igen. Använd TVE Dashboard för att registrera det angivna programmet. |
|  | *unknown_integration* | 400 | Integrationen mellan den angivna programmeraren och identitetsleverantören finns inte. Använd TVE Dashboard för att skapa den nödvändiga integreringen. |
|  | *unknown_software_statement* | 401 | Programsatsen som är associerad med åtkomsttoken känns inte igen. Kontakta supportteamet för att klargöra programvarans status. |
| application-registration | *access_token_expirate* | 401 | Åtkomsttoken har gått ut. Programmet bör uppdatera åtkomsttoken enligt API-dokumentationen. |
|  | *invalid_access_token_signature* | 401 | Åtkomsttokensignaturen är inte längre giltig. Programmet bör uppdatera åtkomsttoken enligt API-dokumentationen. |
|  | *invalid_client_id* | 401 | Den associerade klientidentifieraren känns inte igen. Programmet bör följa den programregistreringsprocess som anges i API-dokumentationen. |
| autentisering | *authentication_session_expirate* | 410 | Den aktuella autentiseringssessionen har gått ut. Användaren måste autentisera på nytt med en MVPD som stöds för att kunna fortsätta. |
|  | *authentication_session_missing* | 401 | Autentiseringssessionen som är associerad med denna begäran kunde inte hämtas. Användaren måste autentisera på nytt med en MVPD som stöds för att kunna fortsätta. |
|  | *authentication_session_invalidated* | 401 | Autentiseringssessionen ogiltigförklarades av identitetsleverantören. Användaren måste autentisera på nytt med en MVPD som stöds för att kunna fortsätta. |
|  | *authentication_session_Issu_mismatch | 400 | Auktoriseringsbegäran misslyckades på grund av att det angivna MVPD-värdet för auktoriseringsflödet skiljer sig från det som utfärdade autentiseringssessionen. Användaren måste autentisera på nytt med önskat MVPD för att kunna fortsätta. |
|  | *authentication_deny_by_hba_policies* | 403 | MVPD har returnerat ett beslut om att neka, på grund av hembaserade autentiseringsprinciper. Den aktuella autentiseringen erhölls med ett hembaserat autentiseringsflöde (HBA), men enheten är inte längre hemma när den begär auktorisering för den angivna resursen. Användaren måste autentisera på nytt med en MVPD som stöds för att kunna fortsätta. |
|  | *identity_not_recognized_by_mvpd* | 403 | Auktoriseringsbegäran misslyckades på grund av att användaridentiteten inte kändes igen av MVPD. |
| auktorisation | *auktorisering_utgången* | 410 | Den tidigare auktoriseringen för den angivna resursen har gått ut. Användaren måste skaffa en ny auktorisering för att kunna fortsätta. |
|  | *authentication_not_found* | 404 | Det gick inte att hitta någon auktorisering för den angivna resursen. Användaren måste skaffa en ny auktorisering för att kunna fortsätta. |
|  | *device_identifier_mismatch* | 403 | Den angivna enhetsidentifieraren matchar inte auktoriseringsenhetsidentifieringen. Användaren måste skaffa en ny auktorisering för att kunna fortsätta. |
| försök igen | **network_connection_error** | 403 | Ett anslutningsfel uppstod med den associerade partnertjänsten. Ett nytt försök att utföra begäran kan lösa problemet. |
|  | *network_connection_timeout* | 403 | En timeout uppstod för anslutningen till den associerade partnertjänsten. Ett nytt försök att utföra begäran kan lösa problemet. |
|  | *network_receive_error* | 403 | Det uppstod ett läsfel när svaret skulle hämtas från den associerade partnertjänsten. Ett nytt försök att utföra begäran kan lösa problemet. |
|  | *maximum_execution_time_överstigen* | 403 | Begäran slutfördes inte inom den tillåtna maxtiden. Ett nytt försök att utföra begäran kan lösa problemet. |
| försök igen efter | *för_många_begäranden* | 429 | För många begäranden har skickats inom ett givet intervall. Programmet kan försöka utföra begäran igen efter den föreslagna tidsperioden. |
|  | *user_rate_limit_pped* | 429 | För många begäranden har utfärdats av en viss användare inom ett givet intervall. Programmet kan försöka utföra begäran igen efter den föreslagna tidsperioden. |
