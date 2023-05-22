---
title: Översikt över PDF-filer
description: Översikt över PDF-filer
exl-id: b918550b-96a8-4e80-af28-0a2f63a02396
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---

# En översikt över flerkanalsprogrammeringsprogram {#mvpd-overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion {#intro}

Den här översikten är avsedd för distributörer av flerkanalsvideo (MVPD). Ytterligare dokumentation, inklusive Kickstart- och Integreringsguider, finns i avsnittet Relaterad information i slutet av det här dokumentet.



TV Everywhere (TVE) är den nu välkända branschrörelsen som gör det möjligt för Pay TV-prenumeranter att få tillgång till innehåll de redan betalar för, på flera enheter, både i och utanför sina hem.  För leverantörer av betal-TV skapar TVE nya möjligheter, både för att bevara befintliga kundrelationer och för att möjliggöra nya. Men tillsammans med dessa möjligheter finns det utmaningar. I TVE-landskapet tillhandahåller programmerare innehållet, men programmerarna innehåller kundinformation som verifierar att potentiella tittare är giltiga prenumeranter.



Det kan vara enkelt att samordna autentisering och behörighet av tittare med en programmerare, men det blir allt mer komplicerat att samordna med dussintals eller hundratals olika programmerare. Men med Adobe® Pass behöver programmeringsleverantörer bara implementera en enda, enkel integrering för att få tillgång till hela TVE-ekosystemet, inklusive programmerare som NBCUniversal Media, Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks, Hulu och så vidare.  Adobe Primetime-autentisering är ett integreringsramverk som gör det enkelt och säkert att avgöra användarnas behörighet.



Underrad: Adobe Primetime-autentisering förmedlar på ett säkert sätt berättigandetransaktioner mellan programmerare och distributörer av videoprogrammeringstjänster, vilket underlättar läsarens åtkomst till prenumerationsinnehåll. Med andra ord gör Adobe Primetime autentisering det enkelt och snabbt för rätt kunder att få tillgång till rätt innehåll.


Med Adobe Primetime-autentisering får MVPD:

Enkel integrering med programmerare.  Leverera direktanslutning från flera innehållsägare med en enda integrering.

Förbättrat kundengagemang.  Stöd för en smidig varumärkesanpassad upplevelse när kunderna ser innehåll på flera plattformar och enheter.

Säker autentisering.  Se till att endast behöriga användare och enheter får tillgång till premiuminnehåll och (valfritt) begränsa antalet enheter och samtidiga strömmar som kan anslutas per hushållskonto.

## Vanliga frågor {#faq}

Hur säker är Adobe Primetime autentisering? Den främsta prioriteten med Adobe Primetime autentiseringsarkitektur är att säkerställa att endast behöriga tittare autentiseras och beviljas åtkomst till premiuminnehåll. Adobe Primetime autentisering binder åtkomsten till visningsenheter och kan bidra till att begränsa strömmar, sessioner och/eller enheter för ett visst hushåll.


Krävs Flash Player? Adobe Primetime autentisering för TV Everywhere är en spelare- och plattformsoberoende som integreras med alla uppspelningsapplikationer, inklusive Silverlight och HTML5. Dessutom har Adobe Primetime-autentisering inbyggt stöd för enheter som telefoner och surfplattor som kör iOS och Android.


Vilka enheter stöder Adobe Primetime autentisering? Adobe Primetime-autentisering stöds av praktiskt taget alla enheter med webbpaketet HTML 5 för visning i webbläsare. Dessutom fortsätter Adobe Primetime-autentisering att lansera SDK:er (Software Development Kits) för olika enhetsspecifika plattformar, bland annat iOS, Android™, Xbox360 (Borttagen) och Adobe Air® (borttagen). Nyligen har Adobe Primetime-autentisering tagit fram en klientlös lösning för enheter som inte kan återge webbläsarsidor (till exempel&quot;smarta&quot; tv-apparater, digitalboxar och spelkonsoler).  Möjligheten att återge webbläsarsidor är ett krav för att autentisera användare med PDF-filer.


Har Adobe Primetime autentisering stöd för de nya standarderna för TV Everywhere? Adobe Primetime-autentisering är kompatibelt med specifikationen CableLabs OLCA (Online Content Access), som innehåller tekniska krav och arkitektur för leverans av video till en Pay TV-kund från onlinekällor. Adobe deltog i det gemensamma CableLabs-projektet för interopt-testning i juni 2011 och klarade testprocessen för en implementering av en tjänsteleverantör. Adobe Primetime-autentisering verifieras (slutförd och testad) mot OLCA-specifikationerna för autentisering. Auktoriseringskomponenten är slutförd, men testverifieringen väntar på att CableLabs-testmiljön ska släppas. Adobe är också en aktiv medlem av OATC (Open Authentication Technical Consortium) och deltar i flera av underkommittéernas projekt för att utarbeta specifikationer som en del av detta organ.



Vad är autentisering? Autentisering är den process där ett MVPD bekräftar att en viss användare är en känd kund.



Vad är auktorisering? Auktorisering är den process där en MVPD bekräftar att en autentiserad användare har en giltig prenumeration på en viss resurs.



## Arkitektur {#architecture}

Adobe Primetime-autentisering är en värdtjänst som möjliggör snabb serverintegration (server till server) baserat på de affärsregler som krävs av både programmerare och distributörer. Detta innebär en snabb time to market för alla parter, en säkrare miljö för att förhindra bedrägerier och en överlägsen kundupplevelse, med mer TV-innehåll tillgängligt för fler personer över flera plattformar.


Adobe Primetime autentisering erbjuds via SaaS-modellen (Software as a Service) och möjliggör säkrare kommunikation mellan slutanvändare, distributörer och programmerare för att validera rätten till innehåll. Huvudkomponenterna i tjänsten omfattar följande:

Serversidan - Den värdbaserade Adobe Primetime-autentiseringsservern. Det här är en programserver som engagerar i kommunikation bakkanal (server-till-server) med autentiseringssystemen i MVPD-program.
Klientsida: Åtkomstaktivering på klientsidan - Åtkomstaktiveraren är en liten fil som läses in i programmerarens webbsida eller spelarprogram. Den ger berättigande API:er till programmerarens visningsprogram och kommunicerar med Adobe Primetime autentiseringsserver.
Klientlösa webbtjänster (för icke-webbkompatibla enheter) - RESTful-webbtjänster som tillhandahåller berättigande API:er för enheter som Smart TV, spelkonsoler och digitalboxar.

>[!NOTE]
>
>Som ett MVPD-program måste dina webbtjänster kunna känna igen begäranden om autentisering och auktorisering från Adobe Primetime-autentisering och svara med nödvändiga data i det förväntade formatet.

Med Adobe Primetime-autentisering kan du förse kunderna med federerad identitetshantering, som också kallas autentisering och auktorisering för enkel inloggning (SSO). Med Adobe Primetime-autentisering behöver abonnenterna inte logga in igen efter den första autentiseringen, så länge som autentiseringen tillåts av MVPD. (Vanligtvis 30 dagar.) För att uppnå detta tillhandahåller Adobe Primetime-autentisering en gemensam domän för autentiseringstoken för våra kunder. Den här informationen om autentiseringstillstånd är tillgänglig för alla deltagande webbplatser som är integrerade med ett visst MVPD.


För närvarande använder de flesta Adobe Primetime-autentiseringsintegreringar med MVPD-program SAML-protokollet, en av de primära autentiseringsstandarderna. Adobe Primetime-autentisering fungerar som proxytjänsteleverantör i SAML-arkitekturen och behåller SAML-autentiseringssvaret som en säker token i den gemensamma domänen Adobe. Adobe Primetime-autentisering är SAML 2.0-kompatibel. Även om Adobe Primetime-autentisering i nuläget vanligtvis används med SAML SSO-lösningar är Adobe Primetime autentiseringsarkitektur inte bunden till något specifikt protokoll. Därför kan stöd för nya protokoll, t.ex. ett som är baserat på OAuth 2.0 eller anpassade protokoll, läggas till över tid.


Adobe samarbetar med en tekniker i MVPD för att konfigurera Adobe Primetime-autentiseringen så att den uppfyller alla befintliga integrationers behov. Integreringen är kostnadsfri för distributörer av videoprogrammeringstjänster och förutsätter en&quot;standard&quot;-integrering och minimala supportkrav (dokumentation och grundläggande support via e-post). Om ett MVPD-dokument kräver betydande support eller en upptrappad tidslinje kan en supportavgift debiteras, eller så kanske leverantören vill arbeta med en tredje part som är bekant med vår lösning, som Synacor.


Adobe Primetime-autentisering stöder även effektiv hantering av affärslogik i MVPD enligt följande:

För affärslogik som är självständig och kan tillämpas av MVPD när en begäran om tillstånd tas emot, tillhandahåller Adobe de data som krävs för att stödja indrivningen av affärslogiken när ett dokument för dokumentskydd tar emot en begäran om auktorisation. Dessa data kan omfatta, men är inte begränsade till, det unika enhets-ID som användaren som gör begäran och enhetens IP-adress har.

För affärslogik som kräver användaråtgärder och/eller specifik hantering av Adobe kan Adobe behålla vissa anpassade egenskaper för varje separat programmeringsfönster. Dessa MVPD-specifika konfigurationer/profiler inkluderar aktivering av fördefinierade arbetsflöden som kan startas vid specifika punkter i arbetsflödet på den översta nivån. Kontakta din Adobe-representant om du vill ha mer information om stöd för anpassade egenskaper.

I följande diagram visas relationen mellan MVPD och Programmer och dessa Adobe Primetime-autentiseringskomponenter:

![](assets/high-level-architecture-nflows.png)

*Bild: Arkitektur och flöden på hög nivå*

## Adobe Primetime-autentiseringskomponenter {#components}

Nedan ges en översikt över några av huvudkomponenterna i Adobe Primetime-ekosystemet för autentisering. Bland dessa finns:

* [Åtkomstaktivering/klientlösa webbtjänster](#ae)
* [Backend-servern som är värd för Adobe](#backend)
* [Tokens](#tokens)

### Åtkomstaktivering/klientlösa webbtjänster {#ae}

Åtkomstaktiveraren underlättar all autentisering och auktoriseringsinteraktion med användaren och körs lokalt på användarens system. Det är åtkomstfunktionen som hanterar de faktiska tillståndsarbetsflödena med MVPD, medan programmeraren behåller ansvaret för webbsidan eller spelarprogrammet på den högre nivån.

Klientlösa webbtjänster tillhandahålls genom Adobe Primetime-autentisering för enheter som inte kan återge webbsidor.  För dessa enheter initieras tillståndsprocessen och innehåll visas på den smarta enheten, medan autentiseringen med en MVPD sker på en webbkompatibel enhet (dator, smarttelefon och surfplatta).

Åtkomstfunktionen:

* Initierar MVPD-specifika autentiserings- och auktoriseringsarbetsflöden.
* Cachelagrar de lyckade auktoriseringssvaren per programmerarresurs/kanal för att minimera onödig trafik på begäran.
* Kan konfigureras för fördefinierade arbetsflöden som är specifika för varje MVPD, till exempel explicit enhetsregistrering.
* Det finns i följande former:
   * En SWF-fil som kan köras i Flash Player
   * En JS-fil som körs direkt av webbläsaren
   * En inbyggd åtkomstfunktion för olika plattformar, inklusive iOS, Android och Xbox.

### Backend-server som är värd för Adobe {#backend}

Adobe Primetime-serverdelsserver för autentisering, värd: Adobe:

* Tillhandahåller autentiserings- och auktoriseringsarbetsflöden med de MVPD-program som kräver server-till-server-kommunikation mellan Adobe Primetime-autentisering och operatorn.
* Upprätthåller konfigurationen för programmerarplatser och program.
* Värdar för komponentfilerna för åtkomstaktivering.
* Skapar autentiserings- och auktoriseringstoken.

### Tokens {#tokens}

Lösningen för berättigande av Adobe Primetime-autentisering är inriktad på att skapa specifika datadelar som hämtas när autentiserings-/auktoriseringsarbetsflödena har slutförts. Dessa datadelar kallas för tokens. De har begränsad livslängd och lagras säkert på plattformsberoende platser. När tokens förfaller måste de utfärdas på nytt genom att autentiserings- och/eller auktoriseringsarbetsflödena återupptas.

Det finns tre typer av tokens som utfärdas under arbetsflödena för autentisering/auktorisering. Två&quot;långlivade&quot; ger kontinuitet i användarens tittarupplevelse. Den tredje, som är en kortlivad variabel, ger stöd för branschens bästa metoder för att minska bedrägerier genom strömrippning. TTL-värdena (time-to-live) för tokens ställs in baserat på avtal mellan MVPD och programmerare. Ni bestämmer er för ett TTL-värde som passar er verksamhet och era kunder bäst.

**Den långvariga autentiseringstoken**. Autentiseringen är klar när en kund använder Adobe Primetime-autentisering för att logga in på sitt MVPD-konto. Adobe Primetime-autentisering skapar sedan en token för långvarig autentisering (&quot;authN&quot;) som är kopplad till den begärande enheten och (beroende på MVPD) en globalt unik identifierare (&quot;GUID&quot;) som identifierar användaren anonymt.

**Den långvariga auktoriseringstoken**. När auktoriseringen är klar skapar Adobe Primetime-autentiseringen en token för långvarig auktorisering (&quot;authZ&quot;). Denna token är inte portabel eftersom den är kopplad till den begärande enheten och en specifik skyddad resurs (t.ex. en kanal, serie eller avsnitt). Access Enabler använder den långvariga authZ-token för att skapa de kortlivade medietoken som används för visningsåtkomst.

**Den kortlivade medietoken**. När användaren har auktoriserats genererar Adobe Primetime-autentiseringen en authZ-token och använder denna token för att generera en kort medietoken som signeras av Adobe och krypteras för att undvika manipulering under utbytet. Eftersom den kortlivade variabeln exponeras för inbäddningsplatsen via antingen API:t för åtkomstaktivering eller klientlösa webbtjänster måste programmerarens medieserver, innan de ger åtkomst till den skyddade resursen, använda en Adobe Primetime-autentiseringskomponent, medietokentverifieraren, för att validera variabeln.

## MVPD-integreringslivscykel {#lifecycle}

Följande bild visar livscykeln för integreringen mellan Adobe Primetime-autentisering och ett MVPD.

![](assets/mvpd-int-lifecycle.png)

*Bild: Integreringslivscykel för MVPD*

## Tillståndsflödesschema {#chart}

I följande flödesdiagram visas den övergripande processen för att bekräfta berättigandet med hjälp av Adobe Primetime-autentisering:

![](assets/authn-authz-entitlmnt-flow.png)

*Bild: Process för att bekräfta tillstånd med hjälp av Adobe Primetime-autentisering*

## Autentiseringssteg {#authn-steps}

I följande steg visas ett exempel på autentiseringsflödet för Adobe Primetime.  Detta är den del av tillståndsprocessen i vilken en programmerare avgör om användaren är en giltig kund till ett MVPD.  I det här scenariot är användaren en giltig prenumerant på ett MVPD.  Användaren försöker visa skyddat innehåll med en programmerares Flash-program:

1. Användaren bläddrar till programmerarens webbsida, som läser in programmerarens Flash-program och Adobe Primetime Authentication Access Enabler-komponenterna på användarens dator. Programmet Flash använder Access Enabler för att ange programmerarens identifiering med Adobe Primetime-autentisering, och Adobe Primetime-autentiseringar använder Access Enabler med konfigurations- och lägesdata för den programmeraren (&quot;begäraren&quot;). Åtkomstaktiveraren måste ta emot dessa data från servern innan andra API-anrop kan utföras.  Teknisk anmärkning: Programmeraren anger sin identitet med åtkomstaktiverarens `setRequestor()` metod, mer information finns i [Integreringshandbok för programmerare](/help/authentication/programmer-integration-guide-overview.md).
1. När användaren försöker visa programmerarens skyddade innehåll, visar programmerarens program användaren en lista med distributörer (MVPD) som användaren väljer en leverantör från.
1. Användaren omdirigeras till en Adobe Primetime-autentiseringsserver, där en krypterad SAML-begäran för det användarvalda MVPD skapas. Denna begäran skickas som en autentiseringsbegäran för programmeraren till MVPD. Beroende på vilket system som används i MVPD dirigeras användarens webbläsare sedan antingen till webbplatsen för MVPD för att logga in, eller så skapas en iFrame-inloggning i programmerarens app.
1. I båda fallen (omdirigering eller iFrame) accepterar MVPD begäran och visar sin inloggningssida.
1. Användaren loggar in med MVPD, MVPD validerar användarens status som betalande kund och sedan skapar MVPD en egen HTTP-session.
1. När användaren valideras skapar MVPD ett svar (SAML &amp; encrypted) som MVPD skickar tillbaka till Adobe Primetime-autentiseringen.
1. Adobe Primetime-autentisering tar emot MVPD-svaret, ser till att en HTTP-session för Adobe Primetime-autentisering är öppen, validerar [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) svar från MVPD och dirigerar om till programmerarens webbplats.
1. Programmerarens webbplats läses in igen, Access Enabler läses in igen och programmeraren anropar setRequestor() igen.  Det andra anropet till setRequestor() är nödvändigt eftersom den aktuella konfigurationen har ändrats - det finns nu en flagga som informerar Access Enabler om att en AuthN-token väntar på att genereras på servern.
1. Åtkomstaktiveraren ser att det finns en väntande autentisering och begär token från Adobe Primetime autentiseringsserver. Token hämtas från servern genom att Flash Player DRM-funktionerna anropas.
1. AuthN-token lagras i programmerarens Flash Player LSO-cache. autentiseringen är nu klar och sessionen tas bort från Adobe Primetime autentiseringsserver.

## Auktoriseringssteg {#authz-steps}

Följande steg fortsätter från föregående avsnitt ([Autentiseringssteg](#authn-steps)):

1. När användaren försöker få åtkomst till programmerarens skyddade innehåll söker programmerarens program först efter en AuthN-token på användarens lokala dator eller enhet.  Om den variabeln inte finns där, [Autentiseringssteg](#authn-steps) ovanstående följs.  Om AuthN-token finns där, fortsätter auktoriseringsflödet med programmerarens program som startar ett anrop till Access Enabler med en begäran om att få användarens visningsrättigheter för ett visst objekt med skyddat innehåll.
1. Den specifika posten med skyddat innehåll representeras av en &quot;resursidentifierare&quot;.  Detta kan vara en enkel sträng eller en mer komplex struktur, men i vilket fall som helst avtalas om resursidentifierarens typ i förväg mellan Programmeraren och det virtuella dokumentationsdokumentet.  Programmerarens program skickar resursidentifieraren till Access Enabler.  Åtkomstaktiveraren söker efter en AuthZ-token på användarens lokala dator eller enhet.  Om AuthZ-token inte finns där, skickar Access Enabler begäran till Adobe Primetime-autentiseringsserver i serverdelen.
1. Adobe Primetime autentiseringsserver kommunicerar med MVPD:s auktoriseringsslutpunkt med hjälp av standardiserade protokoll.  Om svaret från MVPD anger att användaren har rätt att visa det skyddade innehållet, skapar Adobe Primetime autentiseringsserver en AuthZ-token och skickar tillbaka den till Access Enabler, som lagrar AuthZ-token på användarens dator.
1. Med en AuthZ-token lagrad på användarens dator eller enhet anropar programmerarens program Access Enabler för att erhålla en Media Token från Adobe Primetime autentiseringsserver och tillhandahåller denna token till programmerarens program.
1. Slutligen använder programmerarens program Media Token Verifier-komponenten för att bekräfta att rätt användare visar rätt innehåll, och med Media Token på plats tillåts användaren att visa det skyddade innehållet.

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Primetime authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
