---
title: IQ-ordlista för konto
description: 'En ordlista med produktterminologier.  '
source-git-commit: 8d8aa00d693b1ca7f960a71b40053e47249c63e4
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# Produktbegrepp och ordlista {#glossary}

Se följande produktterminologier och deras definitioner.

## Sannolikhet för kontodelning {#account-sharing-probability-def}

En kontrollpanel med diagram som delar upp de aktuella segmenten i kategorier som Mycket låg, Låg, Måttlig, Hög och Mycket hög.

## Åtgärd {#action-def}

En direkt eller indirekt händelse som är associerad med en [Åtgärd](#operation-def) som påverkar egenskaperna (t.ex. Delningspoäng eller antal enheter som används) för ett relaterat åtgärdssegment (eller kohort).

## Aggregerad delningspoäng {#sharing-probability-level-def}

En kontrollpanel med diagram som delar upp de aktuella segmenten i kategorier som Mycket låg, Låg, Måttlig, Hög och Mycket hög, tillsammans med varje kategori i procent av den totala mängden direktuppspelning för segmentet.

## AuthN {#authn-def}

Autentisering, eller antalet autentiseringsförsök. Ett autentiseringsförsök är den process genom vilken en användare utan ett giltigt autentiseringstillstånd omdirigeras till sitt valda MVPD, där han eller hon identifierar sig för MVPD - vanligtvis med ett användarnamn och lösenord.

## AuthN OK {#authn-ok-def}

Antal lyckade autentiseringar. En lyckad autentisering inträffar när en användare identifierar sig genom ett MVPD-dokument och leder till att användaren omdirigeras tillbaka till programmerarappen eller -platsen.

## AuthZ {#authz-def}

Auktorisering, eller antalet begäranden om auktorisering. En begäran om behörighet är den process genom vilken en programmerare begär tillstånd från en MVPD via Adobe att börja direktuppspela en användares begärda innehåll. MVPD tilldelar vanligtvis begäran baserat på de innehållsrättigheter som är kopplade till användarens MVPD-prenumeration (t.ex. om kanalen som är kopplad till innehållet finns i användarens prenumeration). Vissa svar på begäran om tillstånd cachas av Adobe, vilket gör att Adobe kan svara direkt utan att skicka begäran vidare till det enhetliga dokumentationsdokumentet.

## AuthZ OK {#authz-ok-def}

Antal godkända auktoriseringar.

## Kanal {#channel-def}

Channel, som också kallas Property, är en tematiskt relaterad källa för videoinnehåll. Traditionellt representera en distinkt, numeriskt adresserbar kontinuerlig videomatning från ett videoflöde som är av typen MVPD. Kanalen mappas direkt till en tillgänglig innehållskanal som är tillgänglig för prenumeranterna via deras Set Top Box (STB).

## Kluster {#cluster-def}

Ett kluster är en samling platser och enheter. Klustren skapas genom att hitta gemensamma platser mellan olika enheter. De enheter som har setts på en gemensam plats anses tillhöra samma kluster. Två enheter kan finnas i samma kluster även om de inte har gemensamma platser, men kan anslutas via andra enheters platser.

### Mobilkluster {#mobile-cluster-def}

Ett kluster som inte har några statiska enheter.

### Statiskt kluster {#static-cluster-def}

Ett kluster som har minst en statisk enhet.

## Samtidighet {#consurrency-def}

Samstämmigheten definieras av två (eller flera) strömmar som spelas upp samtidigt eller mycket nära i tiden, så att intervallet mellan dem inte kan justeras genom att färdas med normal hastighet.
Samtidig användning beräknas med den maximala hastigheten (engelska mil/tim) mellan två olika kluster. En användare anses ha samtidig användning om han har en hastighet som är större än 124 m/tim på en sträcka som är mindre än 124 miles eller om han har en hastighet som är större än 400 m/tim på en sträcka som är större än 124 miles. Avståndet beräknas mellan platser från olika kluster. Samtidig användning tillåts i samma kluster.

## Enhet {#device-def}

En maskinvaruprodukt för digital video som kan spela upp TV Everywhere-innehåll och som stöds av Adobe Pass. Exempel: smarttelefoner, bärbara och stationära datorer, spelkonsoler och smarta tv-apparater.

## Geografiskt omfång {#geographical-span-def}

Avståndet mellan de längsta punkterna i en uppsättning platser.

## Kornighet {#granularity-def}

Med avseende på tidsram, periodens storlek. som en vecka eller en månad.

## Branschmedelindex {#industry-avg-index-def}

Ett värde som beräknas för var och en av riskindexen (konton, användning, totalt) för alla programmerare och distributörer av videoprogrammeringstjänster under den valda tidsramen.

## IP {#ip-def}

Den Internetprotokolladress som tilldelats en enhet av en Internetleverantör. Till exempel kabelleverantör och cellleverantör.

## Isoleringsläge {#isolation-mode-def}

En typ av delningsanalys där utvärderingen av ett konto är begränsad till händelser som inträffar direkt hos programmerarna i det valda segmentet.  Normalt utvärderas alla kontohändelser, vilket ger en mycket mer korrekt uppskattning av delning.  Vissa MVPD-data är strukturerade på ett sätt som bara tillåter analys av isoleringsläge.

## Plats {#location-def}

En unik punkt på jorden. Det kallas också geopositionering för en specifik spelningsbegäran som identifieras med Pass-data med en precision på 1000mx1000m (en kvadratkm).

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## Medieföretag {#media-company-def}

Media Company är ett företag som äger en grupp medienätverk.

## Mått {#metric}

Metrisk är ett attribut för prenumerantkontot (t.ex. deras MVPD, programmerarna och kanalerna för det innehåll de direktuppspelar, antalet enheter de använder).

## Mobil enhet {#mobile-device-def}

En enhet med hög mobilitet. Till exempel mobiltelefon och surfplatta.

## MVPD {#mvpd-def}

MVPD, som också kallas distributör, är aggregator, återförsäljare och distributör av medieföretagets videoinnehåll.

## Åtgärd {#operation-def}

Åtgärden är en post som skapas för att spåra effekten av en viss [åtgärd](#action-def) på ett associerat segment. Ett exempel på en åtgärd kan vara en gräns för hur många samtidiga strömmar som tillåts för konton som identifieras av segmentet.

## Total delning {#overall-sharing-score}

Ett värde som gör det lättare för användarna att förstå omfattningen av lösenordsdelning på programmeringsegenskaper eller av MVPD-prenumeranter och som gör att de kan agera snabbt på det.

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## Spela upp begäran {#play-requests-def}

En begäran från en klientapp eller webbplats till Adobe om att begära en medietoken för att spela in och skydda en direktuppspelningsstart.

## Programmer {#programmer-def}

Programmer, även kallat Network, är ett företag som är dotterbolag till ett större företag (företag) som äger och förvaltar en eller flera kanaler.

## requestID {#requestorid-def}

Det ID som ett medieföretag använder för att identifiera sig själva eller ett dotterbolag till ett MVPD.  Beroende på programmeringsimplementeringen kan detta mappas till ett medieföretag, en programmerare eller en kanal.  Det vanligaste ID:t ett medieföretag använder för att identifiera sig själva eller ett dotterbolag till ett videofilmsprogram.  Beroende på programmeringsimplementeringen kan detta mappas till ett medieföretag, en programmerare eller en kanal.  Traditionellt är detta mappat till en kanal.  I och med att man skapar pseudokanaler som MML (March Madness Live) och tekniskt drivna åtgärder för att åtgärda MVPD-drivna databegränsningar, har man börjat bli mer kopplad till Media Company.

## resourceID {#resource-id-def}

Innehållet som begärts av slutanvändaren.  Traditionellt har detta identifierat den kanal som är associerad med innehållet som användaren har begärt.  Systemförbättringar gör att det ID:t kan representera specifika program (t.ex. med specifika klassificeringar), och ID:t fortsätter att identifiera den associerade kanalen.

## Riskindex - användning {#risk-index-usage}

Det kallas även Användning från delade konton och är ett värde som beräknas baserat på antalet uppspelningsbegäranden som görs av varje konto, viktat på varje kontos delningssannolikhet. Det kallas även Användning av riskindex för delade konton.

## Segment {#segmet-def}

Segment är en uppsättning konton som uppfyller de användardefinierade villkor som anges av de valda mätvärdena (t.ex. &quot;användare av MVPD A, B, C, D eller E som har bevakat kanalerna X, Y eller Z&quot;).

## Delningsnivå {#sharing-level-def}

Det kallas även riskindex - konton eller riskindex för delade konton, och är ett värde som beräknas baserat på ett genomsnitt av den sannolikhet för delning som beräknats för varje konto i uppsättningen av valda distributörer av virtuella dokumentkonton som har direktuppspelats från en av de valda programmeringskanalerna under den valda tidsramen.

## Statisk enhet {#static-device-def}

En enhet med mycket låg mobilitet. Exempel: spelkonsol, övre ruta och tv-apparat.

## Tidsram {#time-frame-def}

Det kallas även Period- eller Tidsfack och är tidsfönstret som innehåller aktiviteten för uppspelningsbegäran som representeras i användargränssnittet och tabellerna från början till slut.

## MVPD i segment {#top-mvpds-def}

De översta (högst 10) MVPD-värdena i det valda segmentet mäts antingen genom Delningsnivå, Användning från delade konton eller övergripande delningspoäng.

## Trend {#trend-def}

Procentskillnaden i det associerade måttet (till exempel procent av totala uppspelningsbegäranden) mellan den aktuella och föregående perioden.

## Unika prenumeranter {#unique-subscriber-def}

Antalet unika MVPD-konton för en viss period som har interagerat med programmeraren TV Everywhere-appar eller -sajter som involverar Adobe Pass under en viss period.  Interaktionen innefattar all aktivitet i programmeringsappen eller på webbplatsen som leder till ett anrop till en Adobe Pass-tjänst. Du kan till exempel kontrollera authN- eller authZ-tillstånd, autentisera och auktorisera. Det totala antalet unika prenumeranter inkluderar även antalet unika enheter om en programmerare använder Adobe TempPass (kostnadsfri förhandsgranskning) som en del av segmentet.

## Användning {#usage-defs}

### Avid-användare {#avid-user-def}

Mer än 37 spelförfrågningar per månad.

### Ovanliga användare {#infrequent-users-def}

Färre än 9 uppspelningsbegäranden per månad.

### Vanlig användare {#regular-user-def}

Från 9 till 37 uppspelningsbegäranden per månad.

## Användningsmönster {#usage-patern-def}

En av en begränsad uppsättning kategorietiketter som används på ett konto och som bäst karakteriserar kontots användare i form av sociala grupper eller beteenden (t.ex. en liten familj, en resenär eller en dator, social delning osv.).

## Postnummer {#zip-code-def}

The U.S. Postal code associated with locations within the U.S.
