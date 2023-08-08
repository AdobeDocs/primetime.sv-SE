---
title: Anpassade metadata
description: Anpassade metadata
source-git-commit: ac0c15b951f305e29bb8fa0bd45aa2c53de6ad15
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---



# Anpassade metadata {#cm}

>[!NOTE]
>
> Den här sidan är inaktuell eftersom den gäller den tidigare versionen av API som inte längre rekommenderas för nya integreringar

Med tjänsten kan klienter använda både standardfält och anpassade fält i både frågor och beslutsfattande. Standardfälten är alltid tillgängliga för alla strömmar (eftersom de antingen krävs för att skapa strömmar eller genereras av servern):

* program
* mvpd
* accountId
* streamId
* streamStart
* initiator


De anpassade fälten är alla nyckel-/värdepar som skickas vid direktinitiering, antingen som form- eller frågesträngsparametrar. Både standardfält och anpassade fält kan sedan användas i följande scenarier (mer information finns i den faktiska dokumentationen för de berörda API-resurserna nedan):

* Begär extra fält (via fältfrågesträngsparametern) när du hämtar strömlistan för ett konto (resursen /streams)
* Dela upp kontoaktiviteten genom att ange de dimensioner som ska grupperas efter (resursen /activity)
* Definiera principer på serversidan baserat på fältvärden eller kardinaliteter (i exemplen används pseudo-SQL bara för tydlighet):
* Konfigurera en princip som bara ska gälla för specifika fältvärden (t.ex. en dedikerad iOS-princip: WHERE osType IS &#39;iOS&#39;)
* Begränsa antalet distinkta värden för ett visst fält (t.ex. inte mer än X distinkta enheter: HAVING DISTINCT COUNT(deviceId) >= 2)
* Begränsa antalet aktiva strömmar per fältvärde (t.ex. inte fler än X aktiva strömmar för en enskild enhetstyp: GROUP BY deviceType HAVING COUNT(streamId) >= 3)


Olika regler kan fastställas utifrån de nycklar/värden som skickas. Det här kan vara något i den riktningen:

1. Kunden bestämmer att han vill skicka parametergruppen, som får värdena SPORTS och KIDS.
1. Då måste appen göra följande:
   * För sportkanaler skickar appen vid direktinitiering ***type=SPORTS*** som en frågeparameter
   * För kanaler med barnrelaterat innehåll skickar appen vid direktinitiering ***type=KIDS*** som en frågeparameter
1. Därefter kan en sådan policy definieras:
   * `GROUP by type HAVING COUNT(streamID) < 4) IF type=KIDS`
   * `GROUP by type HAVING COUNT(streamID) < 2) IF type=SPORTS`
1. Detta innebär i princip att när en användare ser sport kan han/hon inte göra det på mer än en enhet, men när användaren tittar på barninnehåll tillåts visning på max 3 enheter.

