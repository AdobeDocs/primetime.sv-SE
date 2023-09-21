---
title: Ordlista
description: Ordlista
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---

# Ordlista {#glossary}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## AccessEnabler {#accessEnabler}

Klientkomponenten för Adobe Primetime-autentisering. Adobe Primetime-autentisering tillhandahåller ett AccessEnabler-bibliotek för varje plattform som stöds.

## AuthN {#authn}

Används som kortskrift för autentisering, som i AuthN-token eller AuthN-flöde.


## AuthN-token{#authn-token}

Autentiseringstoken, som genereras av Adobe Primetime-autentisering efter att en användare har autentiserats med ett MVPD. Beroende på programmerarens integrationsplattform lagras token på användarens enhet eller på Adobe Primetime autentiseringsservrar.

## AuthZ {#authz}

Används som kortskrift för&quot;auktorisering&quot;, som i&quot;AuthZ-token&quot; eller&quot;AuthZ-flöde&quot;.

## AuthZ-token {#authz-token}

Autentiseringstoken som genereras av Adobe Primetime-autentisering efter att en användare har auktoriserats att visa skyddat innehåll. AuthZ-token lagras på Adobe Primetime autentiseringsservrar och används för att generera en [Kortlivad medietoken](#short-lived-token).

## Kanal-ID (inaktuellt) {#channel_id}

Tidigare term för resurs-ID.

## Klientlöst API {#clientless-api}

En Adobe Primetime-lösning för autentiseringsintegrering som använder webbtjänster i stället för klientkomponenten AccessEnabler.

## Enhets-ID {#device-id}

Identifierar unikt en enhet (t.ex. en telefon, en surfplatta) inom Adobe Primetime-autentisering. Detta ID hämtas/tillhandahålls av programmerarens program.


## Tillståndsflöde{#entitlement_flow}

Termen som används i Adobe Primetime autentiseringsdokumentation för att hänvisa till hela processen med att registrera en enhet/användare med Adobe Primetime-autentisering, autentisera en användare med ett MVPD, auktorisera en resurs för en användare och logga ut en användare.


## GUID {#guid}

Se [Användar-ID](#user-id).

## IdP {#idp}

Identifiera leverantör; synonym med MVPD i samband med en MVPD-roll i en Adobe Primetime-autentiseringsintegrering. (Kunderna måste verifiera sin identitet via sin Pay TV-leverantörs inloggningssida.)

## Media Token Verifier {#media-token-verifier}

Ett bibliotek som tillhandahålls av Adobe och som används av programmerare för att verifiera den kortlivade medietoken som genereras av Adobe Primetime-autentisering när ett tillståndsflöde har slutförts.

## MVPD {#mvpd}

Distributör av flerkanalsvideo-programmering; synonym med&quot;Betala-tv-leverantör&quot;.

## MVPD-ID {#mvpd-id}

Se [Användar-ID](#user-id).

## Partner-ID {#partner-id}

En identifierare som Adobe skickar till distributörer av videofilmsprogram, som använder den för att identifiera på vars vägnar Adobe Primetime-autentisering begär autentisering. Ibland används det för att konfigurera användargränssnitt för särskilda programmerare, ibland är det samma för alla programmerare, men det beror på programmeringens behov.

## Betala TV-leverantör {#pay-tv-provider}

Synonym med [MVPD](#mvpd).

## Programmer {#programmer}

Synonym med&quot;innehållsleverantör&quot;,&quot;konto&quot;,&quot;kanal&quot;,&quot;tjänsteleverantör&quot;,&quot;varumärke&quot; osv.

## Proxy MVPD {#proxy-mvpd}

Ett MVPD som tillhandahåller identitetstjänster för andra MVPD-program, direkt integrerat med Adobe Primetime-autentisering.

## Proxibel MVPD {#proxied-mvpd}

Ett MVPD som inte är direkt integrerat med Adobe SP, men som är integrerat genom ett MVPD-program.

## Begärande-ID {#requestor-id}

Identifierar unikt en [Programmer](#programmer) (ett konto, varumärke, kanal eller egendom) inom Adobe Primetime autentisering. Detta ID bestäms mellan Programmer och Adobe under den första konfigurationen av kontot. På webben är det begärda ID:t associerat med en uppsättning godkända domäner. Alla anrop som använder ett ID från en extern domän nekas. Programmerare använder också begärande-ID:t för analys. Det finns vanligtvis bara ett begärande-ID per programmerare. Ytterligare en funktion som rör begärande-ID är att programmeraren måste förse Adobe med ett offentligt certifikat, eftersom setRequestor-API-anropet förväntar att krypterade data skickas, som används för att autentisera programmeraren i Adobe Primetime autentiseringssystem.

## Resurs-ID {#resource-id}

En sträng eller mRSS-resurs som identifierar en [Programmer](#programmer) till MVPD. Programmeraren och distributörerna av videoprogrammeringstjänster kommer överens om detta. Adobe Primetime-autentiseringen överför resurs-ID:t utan att ändras, så det måste vara samma för alla videoprogrammeringsmärken. En programmerare kan använda flera resurs-ID:n så länge som programmeringsprofilerna är medvetna om vad varje ID representerar.

## SessionGUID {#sessionGUID}

Se [Användar-ID](#user-id).

## Kortlivad medietoken {#short-lived-token}

Denna token genereras av Adobe Primetime-autentisering när berättigandeprocessen för en viss användare har slutförts. Token skickas till programmeraren som använder Adobe Primetime-verifieringstoken på den kortlivade medietoken för att verifiera säkerheten i tillståndsprocessen.

## Smart enhet {#smart-device}

En term som används i hela Adobe Primetime autentiseringsdokumentation för att hänvisa till digitalboxar, spelkonsoler och smarta tv-apparater. Det är enheter som har nätverksfunktioner men som inte kan återge webbsidor.

## SP{#sp}

Tjänsteleverantör; detta avser vanligtvis *roll* av SP, spelas upp av Adobe Primetime-autentisering, agerar för en programmerare i en integrering med en [MVPD](#mvpd).

## Temporärt pass {#temp-pass}

En funktion som ger programmerare tillfällig kostnadsfri åtkomst till betalinnehåll. Åtkomst är per beställare, för en programmerangiven tidsperiod.

## TTL {#ttl}

Dags att leva. Detta är den angivna tidslängden som en token är giltig.

## TVE {#tve}

TV överallt.

## Användar-ID {#user-id}

Identifierar unikt användaren av en programmerarapp, men härstammar från MVPD. Finns i olika former för olika användningsområden. Se [Användar-ID:n i Programmeröversikten](/help/authentication/programmer-overview.md#user-ids).

## Tillåtelselista {#whitelist}

En lista över domäner som har angetts som berättigade för att kommunicera med Adobe Primetime-autentisering.

## XSTS-token {#xsts-token}

En säkerhetstoken utfärdad av Microsoft för apputveckling för Xbox-konsolen, som används vid autentiseringsintegrering för Xbox/Adobe Primetime.
