---
title: Eskaleringsprocedurer för övervakning av samtidig användning
description: Eskaleringsprocedurer för övervakning av samtidig användning
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---


# Eskaleringsprocedurer för övervakning av samtidig användning {#esc-procedures}

>[!NOTE]
>
>Ring hotline: +1-205-693-9813 och skicka ett e-postmeddelande till `tve-support@adobe.com` inklusive&quot;URGENT - INCIDENT&quot; i ämnesraden.


## Introduktion {#cm-escalation-intro}

I det här dokumentet beskrivs supportförfarandena för större incidenter (**ALLVARLIGHET 1** nivå) som påverkar Adobe Primetime autentisering, Primetime Concurrency Monitoring och dess partners.

## Definition av eskaleringsallvarlighetsgrad 1-nivå {#defn-escl-sevrityone-level}

A **ALLVARLIGHET 1** nivåincident är en **LIVE** situation, **i produktionsmiljön**, som inte tillåter komplettering av autentiserings- och/eller auktoriseringsflödena för en kanal och ett separat programmeringsdokument, vilket påverkar ett stort antal abonnenter av det sidodokument som utför flödet.

## Exempel på incidenter med allvarlighetsgrad 1 {#exampl-sevone-incident}

* Produktionsåtkomstfunktionen finns på <http://entitlement.auth.adobe.com/entitlement/AccessEnabler.js> är inte tillgängligt.

* För ett visst MVPD-dokument dirigerar inte längre Adobe om/visar inloggningssidan efter att användaren har valt MVPD (i någon av webbläsarna som stöds).

* Partnern får ett stort antal rapporter om att användarna inte kan autentisera/auktorisera med ett specifikt MVPD.

* Under autentiseringsprocessen fastnar användaren på en felsida i Adobe utan möjlighet att återinitiera autentiserings-/auktoriseringsflödet.


## Exempel på *NOT* en incident av typen Allvarlighetsgrad 1 {#exampl-not-sev1}

*När det gäller frågor av denna typ kommer Adobe att ge stöd för utredningar, men det rör sig inte om incidenter med allvarlighetsgrad 1:*

* En eller ett fåtal prenumeranter kan inte utföra flödet på grund av ett Flash-versionsproblem (Flash, Flash blockers saknas, fel Flash-version).
* En eller ett fåtal prenumeranter kan inte autentisera sig och finns kvar på inloggningssidan för MVPD.
* En eller några prenumeranter är autentiserade men kan inte spela upp videor.
* Ett/ett fåtal/alla prenumeranter påträffar ett JavaScript-fel på Programmer-webbplatsen.

## Allvarlighetsgrad 1 Eskaleringsflöden {#sevone-escalation-flows}

Allvarlighetsgrad 1-incidenter kan initieras av Adobe eller en Adobe Primetime-autentiseringspartner. Stegen för varje steg visas nedan.

### Partnerinitierat flöde {#partner-initiated-flow}

1. Partnern identifierar en incident av allvarlighetsgrad 1 (som beskrivs ovan) som kräver omedelbar Adobe.

1. Partnern skickar ett e-postmeddelande till tve-support@adobe.com med&quot;URGENT - INCIDENT&quot; på ämnesraden och lägger till följande information:

   * Titel
   * Beskrivning och steg för att återskapa
   * OS
   * Webbläsare
   * Flash version
   * (valfritt) Alla skärmbilder eller videoklipp som visar problemet

1. Om Adobe inte svarar på biljetten inom 30 minuter ringer partnern numret nedan:

   * **1-205-693-9813**


**Om du inte tar med&quot;URGENT-INCIDENT&quot; i biljettens titel hämtas den inte upp av vårt meddelandesystem.**

### Adobe initierat flöde {#adobe-initiated-flow}

**...för ett Adobe Primetime-autentiseringsproblem**

1. Adobe identifierar ett internt problem och öppnar en biljett med vårt spårningssystem.

1. Adobe meddelar sin programansvarige och tekniska kontakt, med angivande av biljettnumret och den beräknade effekten av ärendet.

1. Adobe arbetar för att åtgärda incidenten och håller alla berörda parter informerade.


**...för ett partnerproblem (Programmer/MVPD)**

1. Adobe identifierar ett problem som rör integreringen med ett sidoskydd eller på en av Programmerarens sajter.

1. Adobe meddelar den berörda partnern **följa de stödförfaranden som är i kraft hos den partnern,** och öppnar en biljett med partnerns supportorganisation.

1. Om Adobe under konsekvensanalysen konstaterar att problemet hör till ett av de på förhand överenskomna besluten om incidentscenarier (se avsnittet&quot;Förhandsöverenskomna beslut om incidentscenarier&quot; nedan), kommer det att agera därefter utan att vänta på partnern1. Indata.

1. Adobe väntar på uppdateringar från partnern och ett meddelande från partnern när tjänsten har återställts.

### Föröverenskomna beslut om incidentscenarier {#pre-agreed-decisions}

Det finns vissa situationer då en standardåtgärd kommer att utföras när det aktuella scenariot inträffar:

|    | Scenario | Beskrivning | Åtgärder |
|:---:|:---|:---|:---|
| S1 | Adobe identifierar ett problem med integreringen av ett sidoskydd under normala produktionsåtgärder. | Under normala produktionsåtgärder identifierar Adobe ett problem med en av de alternativa dokumentationsdokumenten som gör det omöjligt att utföra autentiserings-/auktoriseringsflödena (t.ex. utgångna certifikat, utgångna SAML-svar, stängda portar, ändrade parametrar) | Adobe ska underrätta de berörda programmerarna och distributörerna om detta. Adobe kommer att avaktivera denna MVPD för alla berörda programmerare. Adobe kommer att öppna en biljett med det godkända sidoskyddet enligt det överenskomna stödförfarandet med detta sidoskydd |
| S2 | Adobe aktiverar ett nytt MVPD för en programmerare och programmeraren vitlistar MVPD före startdatumet. | Adobe aktiverar ett nytt PDF-dokument för en programmerares webbplats, och webbplatsen visar redan det nya PDF-dokumentet i väljaren, även om det inte var meningen. | Adobe meddelar programmeraren om det nya MVPD-värdet som visas i väljaren före det schemalagda datumet. Programmeraren kommer vid behov att ta bort den från väljaren. |
| S3 | Adobe aktiverar ett nytt MVPD för en programmerare även om MVPD inte är redo att gå i produktion | Adobe aktiverar ett nytt MVPD för en programmerare, men MVPD har ännu inte distribuerat stödet för integreringen så autentiserings-/auktoriseringsflödena kan inte utföras | Adobe kommer endast att genomföra driftsättningen om programmeraren så begär. Programmeraren ansvarar för att vitlistningen av det virtuella dokumentationsdokumentet görs när alla tester har utförts. |

### Förväntningar om respons vid incidenter av allvarlighetsgrad 1 {#response-expectations}

* Inledande svar: 30 minuter (24/7)
* Åtgärdsplan: 1 timme (24/7)
* Upplösning: ASAP (24/7)
