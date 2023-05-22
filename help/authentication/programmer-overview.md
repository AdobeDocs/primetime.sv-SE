---
title: Översikt för programmerare
description: Översikt för programmerare
exl-id: 64a12e49-0ecb-4b81-977d-60c10925bb59
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '4272'
ht-degree: 0%

---

# Översikt för programmerare {#programmers-overview}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Introduktion {#introduction}

Den här översikten är avsedd för den som planerar att integrera Adobe® Pass med sin webbplats eller tillämpning. Mer information, inklusive Kickstart- och Integreringsguider, finns i Relaterad information nedan.

Idag kan era tittare komma ut på internet när som helst, var som helst och begära åtkomst till skyddat innehåll direkt från er, Programmeraren. De vill kanske titta på ett engångsevenemang eller söka rätt till en hel TV-serie som du sänder.

Men innan ni tillåter åtkomst till ert skyddade innehåll måste ni avgöra om kunden har rätt att visa det innehållet. Har de en prenumeration på en distributör av flerkanalsvideo (MVPD)? Om så är fallet, inkluderar prenumerationen din programmering?

Det är inte alltid enkelt för en programmerare att avgöra vilken behörighet en läsare har. MVPD-programmen har behörighet att identifiera data och ge åtkomst till sina kunder.  Lägg till det faktum att tittare som försöker få åtkomst till ditt skyddade innehåll prenumererar på olika typer av videofilmsprogram, som vart och ett har olika system, och det är enkelt att se att det går snabbt att bli komplicerat och tekniskt svårt att avgöra om tittaren har rätt till skyddat innehåll:

![](assets/user-ent-by-progr.png)

*Bild: Användarrättigheter bestäms direkt av programmeraren*

Adobe Primetime autentisering för TV Everywhere förmedlar dessa berättigandetransaktioner mellan programmerare och distributörer av videoprogrammeringstjänster på ett säkert sätt. Adobe Primetime autentisering gör det enkelt, snabbt och säkert för programmerare att tillhandahålla skyddat innehåll till giltiga kunder:

![](assets/user-ent-mediatedby-authn.png)

*Bild: Tillstånd för användare medierat av Adobe Primetime-autentisering*

Adobe Primetime-autentisering fungerar som din proxy i utbyte med medverkande MVPD-program, så att du kan ge tittarna ett enhetligt gränssnitt för olika webbplatser. Med Adobe Primetime autentisering kan du även ge dina tittare autentisering och behörighet för enkel inloggning (SSO). Autentisering och auktorisering spåras för alla deltagande tjänster, så att en prenumerant inte behöver logga in igen efter sin första autentisering på sitt eget system.

* **Autentisering** - Att med ett distributörsdokument bekräfta att en viss användare är en känd kund.
* **Behörighet** - Att bekräfta med ett MVPD att en autentiserad användare har en giltig prenumeration på en angiven resurs.

### Så här fungerar Adobe Primetime Authentication {#HowItWorks}

Programmerarens program för innehållsvisning interagerar med Adobe Primetime-autentisering med klientkomponenten Access Enabler eller RESTful-webbtjänsterna i det klientlösa API:t (för enheter som inte är webbkompatibla, som smarta TV-apparater, spelkonsoler, digitalboxar etc.). Åtkomstaktiveringen körs i användarens system, där alla berättigandearbetsflöden underlättas.  Komponenten Access Enabler hämtas från sin värdsajt på Adobe när kunderna öppnar din sajt och begär skyddat innehåll.  Adobe Primetime autentiseringsservrar är värdar för RESTful-webbtjänster som används i den klientlösa lösningen.

Adobe Primetime-autentisering hanterar de faktiska berättigandearbetsflödena och ger dig samtidigt grundkunskaper som du använder för att:

* Ställa in din identitet. (Programmeraren är&quot;begärande&quot; i berättigandeflödet för Adobe Primetime-autentisering.)
* Autentisera en användare med ett visst MVPD.  (MVPD är identitetsleverantören eller IdP i berättigandeflödet för Adobe Primetime-autentisering.)
* Auktorisera en användare med det virtuella dokumentfönstret för en viss resurs.
* Logga ut användaren.

Programmeraren ansvarar för den översta webbsidan eller spelarprogrammet som utför följande:

* Implementerar användargränssnittet
* Interaktion med Access Enabler eller Clientless API-webbtjänster

Målet med Adobe Primetime-autentisering är att skapa ett enkelt, modulärt sätt för både programmerare och distributörer att hantera verifiering av tillstånd.

## Förstå token {#understanding-tokens}

Lösningen för berättigande av Adobe Primetime-autentisering bygger på generering av specifika datadelar som skapas när autentiserings- och auktoriseringsarbetsflödena har slutförts. Dessa datadelar kallas för tokens. Tokens har begränsad livslängd. När de upphör att gälla måste tokens utfärdas på nytt genom att autentiserings- och auktoriseringsarbetsflödena återupptas.

Mer information om variabler finns i följande avsnitt:

* [Typer av tokens](#token-types)
* [Tokenlagring](#token-storage)
* [Tokensäkerhet](#token-security)
* [Tokendelning](#token-sharing)

### Typer av token {#token-types}

Tre typer av token utfärdas under autentiserings- och auktoriseringsarbetsflödena. AuthN- och AuthZ-tokens är&quot;långlivade&quot;, vilket ger kontinuitet i användarens visningsupplevelse. Media Token är en kortlivad token som ger stöd för branschens bästa metoder för att förhindra bedrägerier genom strömavhämtning. Programmerarna anger TTL-värden (time-to-live) för varje typ av token baserat på avtal som har gjorts med MVPD. Programmerarna bestämmer sig för ett TTL-värde som passar ert företag och era kunder bäst.

* **AuthN-token** (&quot;Långlivad&quot;): Vid lyckad autentisering skapar Adobe Primetime-autentisering en AuthN-token som är kopplad både till den begärande enheten och en globalt unik identifierare (GUID).
   * Adobe Primetime-autentisering skickar AuthN-token till Access Enabler, som cachelagrar den säkert på klientens system.  Även om AuthN-token finns där och ännu inte har gått ut, är den tillgänglig för alla program som använder Adobe Primetime-autentisering. Åtkomstaktiveraren använder AuthN-token för auktoriseringsflödet.
   * Vid ett givet tillfälle cachelagras bara en AuthN-token. När en ny AuthN-token utfärdas och en gammal redan finns, skriver Adobe Primetime-autentiseringen över den cachelagrade token.
* **AuthZ-token** (&quot;Långlivad&quot;): Vid lyckad auktorisering skapar Adobe Primetime-autentisering en AuthZ-token som är associerad med den begärande enheten och en specifik skyddad resurs.  Den skyddade resursen identifieras av ett unikt resurs-ID.
   * Adobe Primetime-autentisering skickar AuthZ-token till Access Enabler, som cachelagrar den säkert på det lokala systemet. Åtkomstaktiveraren använder sedan AuthZ-token för att skapa den kortlivade medietoken som används för visningsåtkomst.
   * Vid en given tidpunkt cachelagras bara en AuthZ-token per resurs. Adobe Primetime-autentisering kan cachelagra flera AuthZ-token, så länge de är kopplade till olika resurser. När en ny AuthZ-token utfärdas och en gammal redan finns för samma resurs, skriver Adobe Primetime-autentiseringen över den cachelagrade token.
* **Medietoken** (&quot;Kortlivad&quot;): Åtkomstaktiveraren använder AuthZ-token för att generera en kort livslängd (standard: 7 minuter) Medietoken. Detta är den punkt där en lyckad uppspelningsbegäran anses ha inträffat.
   * Innan du ger åtkomst till den skyddade resursen måste medieservern använda en autentiseringskomponent från Adobe Primetime, Media Token Verifier, för att validera medietoken.
   * Eftersom medietoken inte är bunden till enheten är dess livslängd betydligt kortare (standard: 7 minuter) än de långvariga AuthN- och AuthZ-tokenerna.
   * Den kortlivade medietoken är begränsad till engångsbruk och cachelagras aldrig. Den hämtas från Adobe Primetime autentiseringsserver varje gång ett auktoriserings-API anropas.

### Tokenlagring {#token-storage}

I Access Enabler lagras långlivade tokens (AuthN och AuthZ) på platser som är specifika för dess miljö:

* **Flash 10.1** (eller högre): De långvariga tokenerna lagras som lokala delade objekt.
* **HTML5**: De långvariga variablerna lagras säkert i webbläsarens lokala lagringsplats i HTML5.
* **iOS**: De långlivade tokenerna lagras på ett beständigt monteringsbord, där de kan nås av andra Adobe Primetime-autentiserings-klientprogram.
* **Android**: De långvariga tokenerna lagras i en delad databasfil, där de kan nås av andra klientprogram för Adobe Primetime-autentisering.
* **Klientlösa API-enheter**: Tokens lagras på Primetimes autentiseringsservrar.

### Tokensäkerhet {#token-security}

Adobe Primetime Authentication Server signerar digitalt alla långlivade token med enhets-ID (härledd från enhetens maskinvaruegenskaper). Den digitala signaturen skiljer sig åt i hur den genereras, skyddas och valideras beroende på miljön:

* **Flash 10.1** (eller senare) - Enhets-ID:t är beroende av enhets-ID:t, ett unikt certifikat som utfärdas av Adobe-servern för personalisering. Säkerheten motsvarar DRM-tekniken i FAXS. Den här valideringen på serversidan jämför det unika enhets-ID:t i token med enhetsautentiseringsuppgifterna (som kommuniceras säkert från Flash Player till Adobe Primetime-autentisering). Enhetens autentiseringsuppgifter identifierar även FAXS-klientversionen och Flash Player (eller AIR)-versionen som den utfärdades till. Enhetens bindning är starkare än med HTML5, så TTL-värdet (time-to-live) för tokens är vanligtvis längre med Flash.
* **HTML5** - Enheten anpassas individuellt på klientsidan. Den använder egenskaper som är tillgängliga via JavaScript för att skapa ett pseudoenhets-ID som innehåller webbläsar- och operativsystemsversioner, en IP-adress och ett webbläsar-cookie-GUID (globalt unik identifierare). Detta enhets-ID jämförs med enhetens pseudoenhets-ID. Eftersom IP-adressen kan ändras vid normal användning, även under samma session, lagras HTML5-token på två platser i Adobe Primetime-autentiseringen: localStorage och sessionStorage. Om IP-ändringarna och sessionStorage-token i övrigt fortfarande är giltiga, behålls sessionen. Med HTML5 är enhetsbindningen inte lika stark, så TTL för tokens är vanligtvis kortare än för Flash.
* **Inbyggda klienter** (iOS och Android) - De långvariga token innehåller information om enhets-ID-personalisering och är därmed bundna till den begärande enheten. Autentiserings- och auktoriseringsbegäranden skickas via HTTPS, och information om enhets-ID signeras digitalt av biblioteket för åtkomstaktivering innan den skickas till serverdelsservrarna. På serversidan valideras enhets-ID-informationen mot den associerade digitala signaturen.
* **Klientlösa API-klienter** - Den klientlösa API-lösningen har en uppsättning säkerhetsprotokoll som innefattar digital signering av alla API-anrop. Token som genereras under tillståndsflödena lagras säkert på Adobe Primetime autentiseringsservrar.

Adobe Primetime-autentisering validerar varje långvarig token för att säkerställa att den enhet som kommer åt innehållet är densamma som den som utfärdade token. För alla tokens säkerställer en validering på klientsidan att den digitala signaturen är intakt och att tokenens integritet bevaras. När validering av enhets-ID misslyckas ogiltigförklaras autentiseringssessionen och användaren uppmanas att logga in igen, vilket återställer tokenerna.

### Tokendelning {#token-sharing}

Program på olika plattformar delar inte ut token. Det finns många skäl till detta, bland annat följande:

* Enligt beskrivning i [Tokenlagring](#token-storage), varierar metoden för att lagra tokens mellan olika plattformar (till exempel Local Shared Objects för Flash, WebStorage för JavaScript).
* Graden av tokensäkerhet skiljer sig mellan olika plattformar. Flash-tokens är till exempel starkt bundna till en enhet med FAXS. Token i en ren JavaScript-miljö har inte samma DRM-stöd som i Flash.  Att dela JS-tokens med Flash-program ökar risken för att mindre säkra tokens utnyttjar en säkrare miljö.

## Programmeringsintegreringslivscykel {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*Bild: Integrera autentisering med programmerarens webbplats och tillämpning*


## Logiska flöden {#logical-flows}

### Tillståndsflödesschema {#chart}

I följande flödesdiagram visas den övergripande processen för att bekräfta berättigandet (med klientkomponenten Adobe Primetime Authentication Access Enabler):

![](assets/ent-flowchart.png)

*Bild: Process för att bekräfta berättigande*

### Autentiseringssteg {#authn-steps}

I följande steg visas ett exempel på autentiseringsflödet för Adobe Primetime.  Detta är den del av tillståndsprocessen i vilken en programmerare avgör om användaren är en giltig kund till ett MVPD.  I det här scenariot är användaren en giltig prenumerant på ett MVPD.  Användaren försöker visa skyddat innehåll med en programmerares Flash-program:

1. Användaren bläddrar till programmerarens webbsida, som läser in programmerarens Flash-program och Adobe Primetime Authentication Access Enabler-komponenterna på användarens dator. Programmet Flash använder Access Enabler för att ange programmerarens identifiering med Adobe Primetime-autentisering, och Adobe Primetime-autentiseringar använder Access Enabler med konfigurations- och lägesdata för den programmeraren (&quot;begäraren&quot;). Åtkomstaktiveraren måste ta emot dessa data från servern innan andra API-anrop kan utföras. Teknisk anmärkning: Programmeraren anger sin identitet med åtkomstaktiverarens `setRequestor()` metod, mer information finns i [Integreringshandbok för programmerare](/help/authentication/programmer-integration-guide-overview.md).
1. När användaren försöker visa programmerarens skyddade innehåll, visar programmerarens program användaren en lista med distributörer (MVPD) som användaren väljer en leverantör från.
1. Användaren omdirigeras till en Adobe Primetime-autentiseringsserver, där en [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) begäran för det användarvalda MVPD skapas. Denna begäran skickas som en autentiseringsbegäran för programmeraren till MVPD. Beroende på vilket system som används i MVPD dirigeras användarens webbläsare sedan antingen till webbplatsen för MVPD för att logga in, eller så skapas en iFrame-inloggning i programmerarens app.
1. I båda fallen (omdirigering eller iFrame) accepterar MVPD begäran och visar sin inloggningssida.
1. Användaren loggar in med MVPD, MVPD validerar användarens status som betalande kund och sedan skapar MVPD en egen HTTP-session.
1. När användaren valideras skapar MVPD ett svar (SAML &amp; encrypted) som MVPD skickar tillbaka till Adobe Primetime-autentiseringen.
1. Adobe Primetime-autentisering tar emot MVPD-svaret, ser att en HTTP-session för Adobe Primetime-autentisering är öppen, validerar SAML-svaret från MVPD och dirigerar om tillbaka till programmerarens webbplats.
1. Programmerarens webbplats läses in igen, Access Enabler läses in igen och programmeraren anropar setRequestor() igen.  Det andra anropet till setRequestor() är nödvändigt eftersom den aktuella konfigurationen har ändrats - det finns nu en flagga som informerar Access Enabler om att en AuthN-token väntar på att genereras på servern.
1. Åtkomstaktiveraren ser att det finns en väntande autentisering och begär token från Adobe Primetime autentiseringsserver. Token hämtas från servern genom att Flash Player DRM-funktionerna anropas.
1. AuthN-token lagras i programmerarens Flash Player LSO-cache. autentiseringen är nu klar och sessionen tas bort från Adobe Primetime autentiseringsserver.

### Auktoriseringssteg {#authz-steps}

Följande steg fortsätter från [Autentiseringssteg](#authn-steps):

1. När användaren försöker få åtkomst till programmerarens skyddade innehåll söker programmerarens program först efter en AuthN-token på användarens lokala dator eller enhet.  Om den variabeln inte finns där, [Autentiseringssteg](#authn-steps) ovanstående följs.  Om AuthN-token finns där, fortsätter auktoriseringsflödet med programmerarens program som startar ett anrop till Access Enabler med en begäran om att få användarens visningsrättigheter för ett visst objekt med skyddat innehåll.
1. Den specifika posten med skyddat innehåll representeras av en &quot;resursidentifierare&quot;.  Detta kan vara en enkel sträng eller en mer komplex struktur, men i vilket fall som helst avtalas om resursidentifierarens typ i förväg mellan Programmeraren och det virtuella dokumentationsdokumentet.  Programmerarens program skickar resursidentifieraren till Access Enabler.  Åtkomstaktiveraren söker efter en AuthZ-token på användarens lokala dator eller enhet.  Om AuthZ-token inte finns där, skickar Access Enabler begäran till Adobe Primetime-autentiseringsserver i serverdelen.
1. Adobe Primetime autentiseringsserver kommunicerar med MVPD:s auktoriseringsslutpunkt med hjälp av standardiserade protokoll.  Om svaret från MVPD anger att användaren har rätt att visa det skyddade innehållet, skapar Adobe Primetime autentiseringsserver en AuthZ-token och skickar tillbaka den till Access Enabler, som lagrar AuthZ-token på användarens dator.
1. Med en AuthZ-token lagrad på användarens dator eller enhet anropar programmerarens program Access Enabler för att erhålla en Media Token från Adobe Primetime autentiseringsserver och tillhandahåller denna token till programmerarens program.
1. Slutligen använder programmerarens program Media Token Verifier-komponenten för att bekräfta att rätt användare visar rätt innehåll, och med Media Token på plats tillåts användaren att visa det skyddade innehållet.


## Registrering och initiering {#reg-and-init}

Det första steget i att arbeta med Adobe Primetime-autentisering är att registrera dig hos Adobe eller hos en av Adobe Primetime auktoriserade partners.

När du registrerar dig anger du en lista över de domäner du ska kommunicera från med Adobe Primetime-autentisering. Domänerna för Turner Broadcasting System omfattar till exempel tbs.com och tnt.tv som Adobe Primetime autentiseringsregistrerade domäner. Var och en av dessa webbplatser får åtkomst till Adobe Primetime-autentisering och tilldelas ett eget begärande-ID (till exempel&quot;TBS&quot; och&quot;TNT&quot;). Om du bestämmer dig för att lägga till ytterligare webbplatser måste du informera Adobe om de ytterligare domännamnen för att få dem placerade i listan över tillåtna domäner och få ytterligare begärande-ID:n.

>[!WARNING]
>
>Kontrollera att testservern finns på en registrerad domän som du tänker använda i produktionen medan du testar integreringen. Begäranden, även testbegäranden, som kommer från icke-godkända domäner ignoreras. Om du t.ex. har begärt att domain.com ska användas i produktionen måste du se till att du distribuerar din testintegration under domain.com, test.domain.com och staging.domain.com.
>
>Begäranden som innehåller användarnamn och/eller lösenord i URL:en ignoreras även om domäner vitlistas. Exempel: `//username@registered-domain/`

Begärar-ID:t identifierar programmerarens klient i all kommunikation med klientkomponenten för åtkomstaktivering för Adobe Primetime-autentisering. Alla statiska data för Adobe Primetime-autentisering som är kopplade till programmeraren är kopplade till detta ID.

>[!TIP]
>
>När du registrerar dig får du förutom ditt begärande-ID även funktionella URL:er för klientkomponenten för Access Enabler och Media Token Verifier.

## Integreringssteg {#integration-steps}

>[!TIP]
>
>Om du använder Adobe Open Source Media Framework (&quot;OSMF&quot;) för din mediespelarutveckling är det snabbaste sättet att använda Adobe Primetime-autentisering att integrera OSMF-pluginen *(Föråldrat)* i spelarens kod.
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [Inställningar för begärande](#requestor)
1. [Hantera autentisering och auktorisering](#authn-authz)
1. [Stöd för enkel utloggning](#ssl)

### 1. Inställningar för begärande {#requestor}

#### 1a. Registrering hos Adobe

Det första steget är att registrera dig hos Adobe eller hos en auktoriserad partner för Adobe Primetime-autentisering.  När du registrerar dig får du en eller flera globalt unika identifierare (GUID). Varje GUID som du får är associerat med en domän från vilken åtkomst tillåts till Adobe Primetime-autentisering. Du skickar ett GUID (kallas begärande-ID) för den begärande domänen för att registrera din identitet för varje session där du interagerar med Access Enabler. Mer information finns i [Registrering och initiering](#reg-and-init) i Programmer Integration Guide.

#### 1b. Inledande integrering av åtkomstaktivering

Nästa steg är att integrera Access Enabler i ditt befintliga mediespelarprogram eller på din webbsida:

* Du kan bädda in Flash-versionen, `AccessEnabler.swf`, i en videospelare baserad på Flash eller så kan du bädda in den direkt i HTML på din webbsida. Du kan kommunicera med Access Enabler SWF i antingen ActionScript eller JavaScript. Bas-API:t är ActionScript, men om du föredrar att arbeta med JavaScript finns det ett fullständigt wrapper-bibliotek som du kan använda på dina sidor.
* För miljöer som inte är Flash kan du:
   * Använd HTML5-/JavaScript-versionen, AccessEnabler.js, och kommunicera med den via JavaScript API
   * Använd AIR Native Extension för Adobe Primetime-autentisering för att kombinera systemspecifik kod med inbyggda ActionScript-klasser
   * Använd en av de inbyggda klientversionerna av Access Enabler-biblioteket (iOS eller Android)

### 2. Hantera autentisering och auktorisering {#authn-authz}

#### 2a. Kommunicera med åtkomstfunktionen

Kommunikationen mellan Access Enabler och webbsidan eller spelarappen är asynkron. Programmet anropar åtkomstaktiveringsmetoder och Access Enabler svarar via återanrop som du registrerar i Access Enabler-biblioteket.

* När ditt program gör en auktoriseringsbegäran initierar Access Enabler automatiskt en autentiseringsbegäran om en giltig AuthN-token inte redan finns på det lokala systemet. När autentiseringen lyckas lagras användarens AuthN-token lokalt, så att användaren inte behöver logga in igen. Om de har autentiserats med Adobe Primetime-autentisering i något annat sammanhang (till exempel via webbplatsen MVPD eller med en annan programmerare) har Access Enabler åtkomst till den lokala AuthN-token och ingen ytterligare autentisering behövs.
* När en användare försöker få åtkomst till ditt skyddade innehåll skickar du en auktoriseringsbegäran till Access Enabler. Efter verifiering (eller initiering) av autentiseringen kontaktar Access Enabler MVPD (via Adobe Primetime autentiseringsserver) för att avgöra om kunden har rätt att visa det skyddade innehållet. Ditt program behöver bara skicka begäran till Access Enabler och sedan hantera svaret (om auktoriseringen lyckades eller misslyckades). Om auktoriseringen lyckas lagras en AuthZ-token på klientsystemet.  Slutligen får ditt program en kort Media-token som du kan använda i din egen autentiseringsprocedur.

>[!NOTE]
>
>* Autentisering sker som SAML-utbyte mellan Adobe Primetime-autentisering som tjänsteleverantör (SP) och MVPD som identitetsleverantör (IdP).
>
>* Auktoriseringen använder ett serverbaserat (server-till-server) webbtjänstutbyte mellan Adobe Primetime-autentisering (SP) och ett MVPD (IdP).



#### 2b. Ange ett berättigandeanvändargränssnitt {#entitlement-ui}

Du anger ett eget användargränssnitt för användaråtkomst till ditt innehåll. Vissa element, till exempel den faktiska inloggningsprocessen, tillhandahålls av MVPD, och vissa element är eventuellt tillgängliga som en del av Adobe Primetime-autentiseringen. Du gör minst följande:

* **Implementera ett MVPD-gränssnitt som gör att en ny användare kan identifiera sitt MVPD och logga in för första gången**. För utveckling har Access Enabler ett grundläggande användargränssnitt som ger kunden möjlighet att välja mellan olika programmeringsskyltar och initierar inloggningsprocessen. För produktion måste du implementera en egen dialogruta för MVPD-väljare. Vissa MVPD-program dirigerar om till sin egen webbplats för inloggning, och vissa kräver att deras inloggningssidor visas i en iFrame. Du måste implementera ett återanrop som skapar denna iFrame för att hantera de fall där användarens MVPD visar sin inloggningssida i en iFrame.
* **Identifiera skyddat innehåll**. Skyddat innehåll kräver åtkomstbehörighet. Gränssnittet bör ange vilket innehåll som skyddas och vilket innehåll som har auktoriserats.  Behörighetsstatus anges ofta med&quot;olåsta&quot; och&quot;låsta&quot; ikoner.
* **Visa att en användare är autentiserad**. Du bör ange en användares autentiseringsstatus som en del av det sätt som du använder för att identifiera skyddat innehåll. Du kan fråga Access Enabler för att avgöra om kunden redan har autentiserats.

#### 2c. Integrera medietokenverifieraren {#int-media-token-ver}

Du måste integrera Adobe Primetime-autentiseringsmedietoken Verifier-komponenten i medieservern.  Detta gör att din befintliga tokenkontrollant kan identifiera de kortlivade medietoken som tillhandahålls av Adobe Primetime-autentisering med en lyckad auktorisering. Verifieraren för medietoken validerar medietoken som det sista säkerhetssteget innan du ger användaren åtkomst till skyddat innehåll. Du får den plats varifrån medietokentverifieraren hämtas när du registrerar dig hos Adobe.

### 3. Stöd för enkel utloggning {#ssl}

I de flesta fall ansvarar mediespelaren för att hantera användarutloggningar via ett enkelt API för åtkomstaktivering. När du anropar logOut() gör Access-funktionen följande:

* Loggar ut den aktuella användaren
* Raderar all autentiserings- och auktoriseringsinformation för den utloggade användaren
* Tar bort alla AuthN- och AuthZ-token från användarens lokala system

Om användaren lämnar datorn inaktiv tillräckligt länge för att tokenerna ska upphöra att gälla, kan användaren fortfarande återgå till sessionen och initiera utloggningen. Adobe Primetime-autentisering säkerställer att alla tokens tas bort och meddelar även MVPD att ta bort deras session.

När utloggningen initieras från en webbplats som inte är integrerad med Adobe Primetime-autentisering kan MVPD anropa tjänsten Adobe Primetime authentication Single Logout via en webbläsaromdirigering.

## Förstå användar-ID:n {#user-ids}

Varje användare som initierar ett tillståndsflöde är kopplad till ett enda unikt användar-ID.  Under ett tillståndsflöde kan dock detta användar-ID presenteras på olika sätt, beroende på vilket API du får ID från.

SessionGUID i Short Media Token är den säkra formen av UserID, som är tillgänglig via anropet sendTrackingData().   I alla aktuella integreringar är detta ett beständigt GUID för användaren över tid och enheter, men GUID-källan börjar med användar-ID:t i SAML-svaret från MVPD.   Men vissa programmeringsgränssnitten kan ändra sig i framtiden och börja skicka ett tillfälligt GUID.  Om en programmerare vill säkerställa att användar-ID:t för MVPD-källan i AuthN-svaret är beständigt, bör de ordna det i sina avtal med MVPD-program.

Här beskrivs olika sätt som användar-ID representeras i Adobe Primetime autentiserings-API:er:

* `sendTrackingData()` GUID-egenskap - Det här är den Adobe-hashade versionen av MVPD UserID.  Det hashas så detta användar-ID kan inte spåras tillbaka till källan från MVPD.   Detta ID är unikt och vanligtvis beständigt, men det går inte att dela det med MVPD för att jämföra specifika användningsbeteenden med vad MVPD har på sin sida.   Den är inte digitalt signerad, så den är inte oåtkomlig för förebyggande av bedrägerier, men den är bra nog för analyser.  Den här formen av användar-ID tillhandahålls på klientsidan för alla händelser som Adobe Primetime-autentisering genererar i AuthN/AuthZ-flödet.
* Korta medietoken `sessionGUID` egenskap - Detta är samma som användar-ID via `sendTrackingData()`Men den här signeras digitalt för att skydda integriteten.  Det gör det här värdet tillräckligt bra för att spåra bedrägeri vid samtidig användning. Den är avsedd att bearbetas på serversidan efter att ha använt vårt valideringsbibliotek och kan analyseras för att upptäcka eventuella bedrägerimönster innan videoströmmen släpps till klienten.  Det är programmeraren som bestämmer om något av detta ska utföras.
* `getMetadata() userID `property - This property will allow Adobe to exponpose the actual source MVPD UserID to the Programmer. Den krypteras med den offentliga nyckeln från certifikatet som vi har från Programmeraren, så att den inte visas för klienten i klartext. Detta ger programmeraren det faktiska användar-ID:t från MVPD, så det är något som kan användas för kontolänkning eller bedrägeriutredning direkt med MVPD.

**Sammanfattning**

* MVPD-användar-ID är ett generellt, men inte garanterat, beständigt unikt ID som **som genererats från PDF:erna och skickats till Adobe om autentiseringen lyckades**. Den är i allmänhet konsekvent i alla nätverk med några undantag.
* MVPD-användar-ID:t innehåller inte PII och är INTE ett kontonummer. Den behöver inte exponeras i krypterad form eftersom vi har validerat med alla dokumentskyddsinspektörer att ingen PII skickas.


Hur du använder användar-ID beror på användningsfallet:

* Om du behöver det för att spåra/analysera är det mest praktiska stället att få det från `sendTrackingData()`.
* Om du behöver det på serversidan för strömfrisläppning, bedrägeri eller driftdata kan du hämta det från Media Token Validator.
* Om du behöver det för kontolänkning och djupare bedrägerier bör du kontakta Adobe för att få reda på om de finns tillgängliga.

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->
