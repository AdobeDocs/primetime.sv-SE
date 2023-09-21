---
title: Eskaleringsprocedurer
description: Eskaleringsprocedurer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# Eskaleringsprocedurer {#escalation-procedures}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

>[!IMPORTANT]
> 
>Ring hotline: **+1-205-693-9813** och mejla till **tve-support@adobe.com** inkluderar **URGENT - INCIDENT** i ämnesraden.

## Introduktion {#introduction}

I det här dokumentet beskrivs supportförfarandena för större incidenter(**ALLVARLIGHET 1** nivå) som påverkar Adobe Primetime autentisering, Primetime Concurrency Monitoring och dess partners.


## Definition av en ALLVARLIGHETSincident på 1-nivå {#definition-of-a-severity-1-level-incident}

A **ALLVARLIGHET 1** nivåincident är en **LIVE** situation, **i produktionsmiljön**, som inte tillåter komplettering av autentiserings- och/eller auktoriseringsflödena för en kanal och ett separat programmeringsdokument, vilket påverkar ett stort antal abonnenter av det sidodokument som utför flödet.


## Exempel på incidenter av typen SEVERITY 1 {#examples-of-severity-1-incidentcs}

* Produktionsåtkomstfunktionen finns på  `https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js` (eller `https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js`) är inte tillgängligt.

* För ett visst MVPD-dokument dirigerar inte längre Adobe om/visar inloggningssidan efter att användaren har valt MVPD (i någon av webbläsarna som stöds).

* Partnern får ett stort antal rapporter om att användarna inte kan autentisera/auktorisera med ett specifikt MVPD.

* Under autentiseringsprocessen fastnar användaren på en felsida i Adobe utan möjlighet att återinitiera autentiserings-/auktoriseringsflödet.


| Exempel på **NOT** en incident av typen Allvarlighetsgrad 1 |
|---|
| När det gäller frågor av denna typ kommer Adobe att ge stöd för utredningar, men det rör sig inte om incidenter med allvarlighetsgrad 1:<ul><li>En eller ett fåtal prenumeranter kan inte utföra flödet på grund av ett problem med Flashens version (Flash saknas, blockering av Flashar, fel Flash).</li><li>En eller ett fåtal prenumeranter kan inte autentisera sig och finns kvar på inloggningssidan för MVPD.</li><li>En eller några prenumeranter är autentiserade men kan inte spela upp videor.</li><li>Ett/ett fåtal/alla prenumeranter påträffar ett JavaScript-fel på Programmer-webbplatsen</li></ul> |

## Allvarlighetsgrad 1 Eskaleringsflöden {#severity-1-escalation-flows}

Allvarlighetsgrad 1-incidenter kan initieras av Adobe eller en Adobe Primetime-autentiseringspartner. Stegen för varje steg visas nedan.

### Partnerinitierat flöde {#partner-initiated-flow}

1. Partnern har identifierat en incident av allvarlighetsgrad 1 (som beskrivs ovan) som kräver omedelbar åtgärd från Adobe.
1. Partnern skickar ett e-postmeddelande till **tve-support@adobe.com** inkluderar **URGENT - INCIDENT** på ämnesraden och lägga till följande information:
   * Titel
   * Beskrivning och steg för att återskapa
   * OS/webbläsare
   * SDK &amp; Version
   * Enheter som påverkas
   * % användare påverkas
   * HTTP-spårning eller enhetsloggar som visar problemet
   * (valfritt) Alla skärmbilder eller videoklipp som visar problemet
1. Om Adobe inte svarar på biljetten inom 30 minuter ringer partnern följande nummer:
   **1-205-693-9813**
   >[!IMPORTANT]
   >Om du inte tar med&quot;URGENT-INCIDENT&quot; i biljettens titel hämtas den inte av vårt meddelandesystem**.

### Adobe-initierat flöde {#adobe-initiated-flow}

#### ...för ett Adobe Primetime-autentiseringsproblem {#adobe-initiated-flow-authn-issue}

1. Adobe identifierar ett internt problem och öppnar en biljett med vårt spårningssystem.

1. Adobe meddelar sin programansvarige och tekniska kontakt med partnern och anger biljettnumret och den beräknade effekten av ärendet.

1. Adobe arbetar för att åtgärda incidenten och håller alla berörda parter informerade.

#### ...för ett partnerproblem (Programmer/MVPD) {#adobe-initiated-flow-partner-issue}

1. Adobe identifierar ett problem som rör integreringen med ett sidoskydd eller på en av Programmerarens sajter.

1. Adobe meddelar den berörda partnern <u>följa de stödförfaranden som är i kraft hos den partnern,</u> och öppnar en biljett med partnerns supportorganisation.

1. Om Adobe under konsekvensanalysen upptäcker att problemet hör till ett av de på förhand överenskomna besluten om incidentscenarier, se **Föröverenskomna beslut om incidentscenarier** fungerar det som det ska utan att vänta på partnerns indata.

1. Adobe väntar på uppdateringar från partnern och ett meddelande från partnern när tjänsten har återställts.

## Föröverenskomna beslut om incidentscenarier {#pre-agreed-descn}

Det finns vissa situationer då en standardåtgärd kommer att utföras när det aktuella scenariot inträffar:

|   | Scenario | Beskrivning | Åtgärder |
|---|---|---|---|
| S1 | Adobe identifierar ett problem med integreringen av ett sidoskydd under normala produktionsåtgärder. | Under normala produktionsåtgärder identifierar Adobe ett problem med en av de alternativa dokumentationsdokumenten som gör det omöjligt att utföra autentiserings-/auktoriseringsflödena (t.ex. utgångna certifikat, utgångna SAML-svar, stängda portar, ändrade parametrar) | - Adobe skall underrätta de berörda programmerarna om detta.  </br> </br> - Adobe kommer att avaktivera denna MVPD för alla berörda programmerare. </br> </br> - Adobe kommer att öppna en biljett med det alternativa dokumentationsdokumentet för dokumentationsskydd som godkänts i enlighet med detta |
| S2 | Adobe aktiverar ett nytt MVPD för en programmerare och programmeraren tillåter MVPD före startdatumet. | Adobe aktiverar ett nytt PDF-dokument för en programmerares webbplats och webbplatsen visar redan det nya PDF-dokumentet i väljaren, även om det inte var meningen. | - Adobe ska meddela Programmeraren om det nya MVPD-programmet som visas i väljaren före det schemalagda datumet. </br> </br>  - Programmeraren kommer vid behov att ta bort den från väljaren. |
| S3 | Adobe aktiverar ett nytt MVPD för en programmerare även om MVPD inte är redo att gå i produktion | Adobe aktiverar ett nytt MVPD för en programmerare, men MVPD har ännu inte distribuerat stödet för integreringen så autentiserings-/auktoriseringsflödena kan inte utföras | - Adobe kommer endast att göra distributionen om programmeraren kräver det </br> </br> - Programmeraren ansvarar för att säkerställa att det mobila dokumentationsdokumentet är godkänt när alla tester har utförts. |

## Förväntningar om respons vid incidenter av allvarlighetsgrad 1 {#response-expectations-for-severity-one-incidents}

* Inledande svar: 30 minuter (24/7)
* Åtgärdsplan: 1 timme (24/7)
* Upplösning: ASAP (24/7)
