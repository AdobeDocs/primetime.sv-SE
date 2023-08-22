---
title: Om Adobe Primetime autentisering och TV Everywhere
description: Om Adobe Primetime autentisering och TV Everywhere
exl-id: 5edeaccb-f9fa-4395-83b4-706c518d5a03
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '6288'
ht-degree: 0%

---

# Om Adobe Primetime autentisering och TV Everywhere {#about-auth-tve}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.

## Om TV Everywhere {#about-tve}

Dagens tv-tittare kan vara online när som helst eller var som helst, och de förväntar sig att de har tillgång till Pay TV-innehåll direkt där. Dessutom visar publiken innehåll med hjälp av allt fler internetkompatibla enheter, bland annat:

* Bärbara
* Surfplattor
* Smartphones
* Webbplatser
* Federerade appar
* Spelkonsoler
* Rutor
* Smarta TV-apparater

TV Everywhere är branschrörelsen som stöder Pay TV-prenumeranters möjlighet att få tillgång till samma innehåll som de redan betalar för, på flera enheter, både i och utanför sina hem. Även om den största delen av tv-tittandet fortfarande förekommer på konventionell, linjär tv är konsumtionstillväxten i tidförskjutet innehåll, onlinevideo och alternativa skärmar. Det innebär att marknaden för videodistribution idag är i ett tillstånd av störningar, och TV Everywhere har blivit en lösning som anpassar programmerarnas, Pay TV-leverantörernas och Pay TV-abonnenternas intressen.


Det tekniska målet för TV Everywhere är att göra det möjligt för Pay TV-kunder att få tillgång till innehåll som de redan prenumererar på på alla sina enheter och plattformar.


Affärsmålen för TV Everywhere är att

* **Bevara befintliga kundrelationer och aktivera nya**
* Låt programmerare och rättighetsinnehavare nå största möjliga publik och få ut mer av det material de lägger ut
* Utvidga varumärken genom direktinteraktion online med tittarna

## Problem med TV Everywhere {#tve-challenges}

Tillsammans med möjligheterna med TV Everywhere kommer utmaningar. Kärnan i detta är berättigande. Innan ett visningsprogram får åtkomst till prenumerationsinnehåll måste någon avgöra om de har rätt till den åtkomsten.

Har användaren en prenumeration hos en Pay TV-leverantör? Om så är fallet, innehåller den prenumerationen det innehåll som begärs? Tillstånd är särskilt svårt för programmerare och innehållsägare att direkt avgöra, eftersom det är Pay TV-operatörerna som har identifieringsdata för sina kunder samt kundernas åtkomstbehörighet.


Förutom berättigande finns en mängd relaterade tekniska utmaningar och integreringsproblem, bland annat:

* Utveckla och implementera en heltäckande strategi för flera enheter
* Samordna de otaliga relationerna mellan programmerare och leverantörer av betal-TV
* Förhindra bedräglig åtkomst till eller missbruk av tjänstvillkor
* En enhetlig och frustrerande autentiseringsprocess för användare på olika webbplatser och i olika appar
* Bevara en snabb time-to-market för att hålla jämna steg med filialavtal
* Hantera kostnader i samband med flera integreringar

Dessa utmaningar gör att du kan utföra och underhålla komplexa, direkta integreringar mellan programmerare och autentiseringssystemen hos flera olika leverantörer av betal-TV mycket resurskrävande, vilket kräver både tid och teknisk finess.


Lösningen? **Autentisering med Adobe® Primetime**.

## Introduktion till Adobe Primetime-autentisering {#authentication-intro}

Med Adobe Primetime autentisering behöver programmerare och betal-TV-leverantörer bara göra en enkel integrering med Adobe Primetime autentiserings-API:er för att få tillgång till hela ekosystemet, inklusive:

* Programmerare som Turner Broadcasting (TBS, TNT, CNN), Fox Broadcast Networks och Hulu

* Alla de främsta leverantörerna av betal-TV i USA, som omfattar över 90 procent av alla hushåll som använder betal-TV

Dessutom har Adobe Primetime autentisering ett ramverk som gör användarautentisering och behörighet enkel och säker.

![](assets/programmers-connect-authn.png)

*Bild 1: Bara några programmerare och leverantörer av betal-TV som ansluter via Adobe Primetime-autentisering...*

Adobe Pass förmedlar på ett säkert sätt berättigandetransaktioner mellan programmerare och betal-TV-leverantörer, vilket underlättar läsarens åtkomst till prenumerationsmaterialet. Eller, med andra ord..

**Adobe Primetime autentisering gör det enkelt och snabbt för rätt kunder att få tillgång till rätt innehåll.**

**Vem är Adobe Primetime autentisering till?**

* **Programmerare** som enkelt vill kunna integreras med leverantörer av betal-TV (även kallade &quot;MVPD&quot; eller &quot;Multichannel Video Programming Distributors&quot;) för att nå största möjliga publik. Med Adobe Primetime autentisering kan programmerare autentisera tittare över alla större leverantörer, oberoende av klientplattform.

* **Betala TV-leverantörer/distributörer av videoprogrammeringsprogram** som vill ha smidiga anslutningsmöjligheter med olika programmerare och nöjdare kunder genom att göra det enklare att få tillgång till prenumerationsinnehåll online.

* **Betala TV-kunder** som vill ha enkel åtkomst till innehåll de redan prenumererar på, var de än befinner sig, utan extra kostnad. Med enkel inloggning får du säker autentisering för visningsprogrammet på webben eller i mobilappar, utan att du behöver ladda ned kunder eller upprepa inloggningar, liksom en bra användarupplevelse.

För **Programmerare**, ger Adobe Primetime-autentisering:

* Enkel integrering och direktanslutning med de bästa Pay TV-leverantörerna, utan att behöva bekymra dig om flera, direkta integreringar
* Optimering av både prenumeration (licensiering) och annonsintäkter genom stöd till en så bred publik som möjligt för innehåll
* Säker autentisering, med tillgång till premiuminnehåll som endast beviljas behöriga användare/enheter
* Ett öppet och flexibelt ramverk som är både spelare- och DRM-plattformsoberoende. Uppspelningen kan ske på en rad olika plattformar, bland annat iOS, Android, Windows 8, spelkonsoler, digitalboxar med mera.
* Kompatibilitet med alla DRM-tekniker, till exempel Adobe Flash Access® eller Play Ready®.
* Stöd för autentisering och auktorisering med enkel inloggning (SSO), så att prenumeranter inte behöver logga in igen efter den första autentiseringen på sina egna system.


För **Betala TV-leverantörer/distributörer av videoprogrammeringsprogram**, ger Adobe Primetime-autentisering:

* Enkel integrering med innehållsägare, vilket ger direktkontakt med flera programmerare med en enda integrering
* Förbättrat kundengagemang genom stöd för en smidig, varumärkesprofilerad upplevelse när de ser innehåll på flera plattformar och enheter
* Säker autentisering som garanterar att endast behöriga användare/enheter får tillgång till premiuminnehåll och (valfritt) begränsar antalet enheter och samtidiga strömmar som kan anslutas per hushållskonto.


För **Betala TV-kunder**, ger Adobe Primetime-autentisering:

* **TV Everywhere!**

Resten av detta dokument innehåller en teknisk introduktion till Adobe Primetime autentisering.  Även om mycket av följande fokuserar på programmeringsintegrering finns det både allmän och specifik information som gäller även leverantörer av betal-TV. Det här dokumentet visar också säkerhet och integritet för hur Adobe Primetime autentisering fungerar som en lösning för TV Everywhere. Mer information finns i denna rapport: kontakta Adobe eller fyll i blanketten Begäran om information [här](https://www.adobe.com/).

## Arkitekturbyggstenar {#arch-building-blocks}

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/import-pc7mz3dfnv/check.gif) Nedan beskrivs de centrala berättigandetransaktionerna för autentisering och auktorisering. Autentisering är processen att med en Pay TV-leverantör bekräfta att en viss användare är en känd kund. Auktorisering är den process där en Pay TV-leverantör bekräftar att en autentiserad användare har en giltig prenumeration på en viss resurs.
Adobe Primetime-autentisering består av följande grundläggande komponenter:

* Klientkomponent (något av följande):

   * Åtkomstaktivering - Ett plattformsspecifikt bibliotek som ger lättanvända API:er och kodexempel för implementering av tillståndsflödena
   * Det klientlösa API:t - RESTful web services; ger slutpunkter för tillståndsflöden för plattformar utan återgivningsmöjligheter för webbsidor (t.ex. spelkonsoler, digitalboxar)

* Serverlösningar som ligger i Adobe
* Verifieraren för medietoken
* A Secure, Central Medium of Exchange (Tokens)

På en grundläggande nivå består Adobe Primetime-autentisering av tre komponenter (Access Enabler, backend-servrar på Adobe och Media Token Verifier) och en central utbytesfunktion (tokens).

### Klientkomponenter {#client-components}

* Åtkomstaktivering
* Klientlöst API

#### Åtkomstaktivering {#access-enabler}

På plattformar som stöds fullt ut (t.ex. webben, iOS, Android och Windows 8) interagerar programmerare med Adobe Primetime autentisering via klientkomponenten för Access Enabler. Den här komponenten underlättar all autentisering och auktoriseringsinteraktion med kunden.  Åtkomstaktiveraren körs lokalt på datorn. När en användare öppnar en programmerarwebbplats eller ett program och begär innehåll, läses den Adobe-baserade/underhållna åtkomstaktiveringskomponenten in i bakgrunden utan att något märks.

Åtkomstaktiveraren hanterar de faktiska tillståndsarbetsflödena, medan Programmeraren behåller ansvaret för webbsidan eller uppspelningsprogrammet på en högre nivå som implementerar användargränssnittet och interagerar med Access Enabler. Dessa interaktioner sker via ett asynkront system med funktioner och återanrop, som definieras av API:t för åtkomstaktivering.

Detta är de grundläggande tillståndsflödena som enkelt kan implementeras med API:t för åtkomstaktivering:

* Ställa in den begärande (programmerarens) identitet
* Kontrollera/hämta användarautentisering mot en viss Pay TV-operatör (&quot;identitetsleverantör&quot;)
* Kontrollerar/hämtar användarauktorisering för en viss resurs
* Loggar ut användaren

Access Enabler tillhandahåller även följande tjänster:

* Den validerar frågor från Programmeraren, inklusive registreringsstatus för specifika klienter, deras domäner och deras resurser/kanaler.
* Den levererar data som skapar listan över Pay TV-operatörer från vilka användaren väljer sin leverantör. Denna lista valideras och definieras som lämplig för den programmerare som begäran kommer från.
* Det initierar Pay TV-operatörsspecifika autentiserings- och auktoriseringsarbetsflöden.
* Den cachelagrar de lyckade auktoriseringssvaren per programmerarresurs/kanal för att minimera onödig trafik på begäran.
* Den kan konfigureras för fördefinierade arbetsflöden som är specifika för varje Pay TV-operatör, till exempel explicit enhetsregistrering.

Beroende på din webbplats eller ditt spelarprogram kan Access Enabler ha följande former:

* En SWF-fil som Flashen Player kan köra
* En JS-fil som körs direkt av webbläsaren
* En inbyggd åtkomstfunktion för plattformar som stöds (iOS, Android och Windows 8)

#### Klientlöst API {#clientless-api}

Det klientlösa API:t är avsett för&quot;smarta enheter&quot; (spelkonsoler, digitalboxar och smarta TV:er) som inte stöder webbläsare (krävs för autentisering med programmeringsgränssnitt).  I den klientlösa metoden kommunicerar smarta enhetsprogram direkt med Adobe Primetime-autentisering via RESTful-API:er för webbtjänster för allt utom autentisering, som utförs i en andra skärmapp (webbläsare). Klientbiblioteket för Access Enabler används alltså inte. Utvecklare av appar för smarta enheter använder i stället Adobe Primetime webbtjänstAPI:er för autentisering för att implementera tillståndsflödena.

### Serverlösningar som ligger i Adobe {#adobe-backend-servers}

Adobe Primetime serverdelsservrar för autentisering, som hanteras av Adobe:

* Tillhandahåll autentiserings- och auktoriseringsarbetsflöden med Pay TV-leverantörer som kräver server-till-server-kommunikation mellan Adobe Primetime-autentisering och operatören.
* Underhåll konfigurationen för programmerarwebbplatser och program.
* Lägg upp komponentfilerna för den hämtningsbara åtkomstaktiveringen.
* Ange RESTful-webbtjänstslutpunkterna för API-integrering utan klient.
* Generera (och i vissa fall lagra) autentiserings- och auktoriseringstoken.

### Token och Media Token Verifier {#tokens-media-token-verifier}

Lösningen för berättigande av Adobe Primetime-autentisering är inriktad på att skapa specifika datadelar som hämtas när autentiserings-/auktoriseringsarbetsflödena har slutförts. Dessa datadelar kallas för tokens. De har en begränsad livslängd och lagras säkert, antingen på plattformsberoende platser på klienten eller på Adobe-servrar när det gäller API-lösningen utan klient. När tokens förfaller måste de utfärdas på nytt genom att autentiserings- och/eller auktoriseringsarbetsflödena återupptas.

Det finns tre typer av token som Adobe Primetime-autentisering ger upphov till under arbetsflödena för autentisering/auktorisering. Två&quot;långlivade&quot; ger kontinuitet i användarens tittarupplevelse. Den tredje, som är en kortvarig variabel, ger stöd för branschens bästa metoder för att minska bedrägerier (där bedrägeri omfattar exempelvis explosioner som strömavhämtning). TTL-värdena (time-to-live) baseras på avtal mellan programmerare och leverantörer av betal-TV, som är överens om ett värde som passar alla bäst.

#### (Long-Lived) Autentiseringstoken {#long-lived-auth-token}

Autentiseringen är klar när en kund använder Adobe Primetime-autentisering för att logga in på sitt Pay TV-konto. Adobe Primetime-autentisering skapar sedan en AuthN-token som är bunden till den begärande enheten och (beroende på Pay TV-leverantören) en globalt unik identifierare (&quot;GUID&quot;) som identifierar användaren anonymt.

* Adobe Primetime-autentisering lagrar AuthN-token säkert på en plats där den är tillgänglig för alla program som använder Adobe Primetime-autentisering. För integreringar med Access Enabler lagras tokens säkert på klientsidan.  Adobe Primetime-autentisering använder AuthN-token för att göra efterföljande autentiseringsfrågor för användarens räkning.
* Vid en given tidpunkt lagras endast en AuthN-token. När en ny AuthN-token utfärdas och en gammal redan finns, skriver den nya token över det befintliga lagrade värdet.

#### (Long-Lived) Authorization Token {#long-lived-authriz-token}

När auktoriseringen är klar skapar Adobe Primetime-autentiseringen en AuthZ-token (long-life authentication). Denna token är inte portabel eftersom den är kopplad till den begärande enheten och en specifik skyddad resurs (till exempel en kanal, serie eller avsnitt).

* Adobe Primetime-autentisering lagrar AuthZ-token säkert tillsammans med andra autentiseringstoken för andra resurser.  Liksom med AuthN-tokens lagras token på plattformar som använder Access Enabler lokalt på klienten. På plattformar som använder Clientless API lagras tokens på Adobe Primetime autentiseringsservrar.
* TTL (time-to-live) för den långlivade AuthZ-token definieras vanligtvis i intervallet dagar till veckor, beroende på det specifika avtalet mellan Pay TV-leverantören och programmeraren.
* Vid en given tidpunkt lagras endast en AuthZ-token per resurs. Det kan finnas flera auktoriseringstoken lagrade, förutsatt att de är kopplade till olika resurser. När en ny auktoriseringstoken utfärdas och en gammal redan finns för samma resurs, skriver den nya token över det befintliga cachelagrade värdet.
* Adobe Primetime-autentisering använder den långvariga AuthZ-token för att skapa de kortlivade medietoken som används för visningsåtkomst.

#### Kortlivad medietoken {#short-lived-media-token}

När Adobe Primetime-autentiseringen genererar AuthZ-token används denna token för att generera en kortlivad medietoken som signeras av Adobe och krypteras för att undvika manipulering under utbyte:

* TTL för den kortlivade token (standard: 5 min) är inställd på att tillåta klocksynkroniseringsproblem mellan servern som genererar token och servern som validerar token.
* Den kortlivade variabeln exponeras för inbäddningsplatsen innan åtkomst ges till den skyddade resursen, så programmeraren måste validera variabeln, använda Media Token Verifier för integreringar med Access Enabler eller Token Verifier Service om API-integreringar utan klient används.

#### Media Token Verifier {#media-token-verifier}

Programmerarna ansvarar för att integrera Media Token Verifier Library i sin befintliga programserver, så att Verifieraren kan utföra slutanvändarens validering innan videoströmmen faktiskt startas. Biblioteket för verifiering av medietoken definierar:

* Ett API för tokenverifiering som hämtar information från token, t.ex. om den är giltig, när token utfärdades och andra relevanta data
* Den offentliga nyckel för Adobe som används för att verifiera att token verkligen kommer från Adobe
* En referensimplementering som visar hur du använder Verifier API och hur du använder den offentliga nyckeln för Adobe i biblioteket för att verifiera dess ursprung

![](assets/high-level-architecture-nflows.png)

*Bild 2: Arkitektur på hög nivå för Adobe Primetime-ekosystemet för autentisering i en Access Enabler-integrering*

## Integrera med Adobe Primetime-autentisering {#integrate-auth}

Oavsett om du är leverantör av betal-TV eller programmerare kräver processen att integrera med Adobe Primetime-autentisering en viss del av ditt aktiva deltagande. Var och en av dessa processer beskrivs nedan.

### Betala-TV-leverantörsprocessen

Betal-TV-leverantören har som huvudansvar att verifiera att en begärande användare verkligen är en känd prenumerant som har rätt att få åtkomst till programmerarens innehåll. På en hög nivå kräver Adobe Primetime autentiseringsprocess för integrering med en ny Pay TV-leverantör följande steg:

1. Leverantören signerar Adobe Primetime NDA (Authentication Non-Disclosure Agreement).
1. Leverantören förser Adobe med specifikationer för sina autentiserings- och auktoriseringssystem. För den enklaste integrationen rekommenderar vi att Pay TV-operatörer har en SAML-baserad identitetsleverantör (IdP) för autentisering och möjlighet att kommunicera via SOAP-åtkomstprotokollet för auktorisering.
1. Leverantören upprättar anslutningsmöjligheter mellan sina servrar och Adobe Primetime autentiseringsservrar. Detta inkluderar att tillhandahålla slutpunkter och att ange IP-adresser.
1. Utgåva före kvalificering och kvalitetsfrågor.
1. Produktionsrelease och Frågor och svar.

Även om Adobe Primetime-autentisering kan ersätta befintliga integreringar för programmerare krävs det vanligtvis inte för betal-TV-leverantörer. Adobe samarbetar med leverantörens tekniska team för att konfigurera Adobe Primetime-autentiseringen så att den uppfyller alla befintliga integrationers behov. Integreringen är kostnadsfri för leverantörer av betal-TV och förutsätter en&quot;standard&quot;-integrering och minimala supportkrav (dokumentation och grundläggande support via e-post). Om en leverantör behöver omfattande support eller en uppskalad tidslinje kan en supportavgift debiteras eller leverantören kanske vill arbeta med en tredje part som är bekant med vår lösning, som Synacor.


Adobe Primetime-autentisering stöder även effektiv hantering av affärslogiken hos Pay TV-leverantören enligt följande:

* För affärslogik som är självständig och kan tillämpas av operatören när en begäran om tillstånd tas emot, tillhandahåller Adobe de data som krävs för att stödja logiska funktioner när operatören tar emot en auktoriseringsbegäran. Dessa data kan omfatta, men kan inte begränsas till, det unika enhets-ID som användaren som gör begäran och enhetens IP-adress har.
* För affärslogik som kräver användaråtgärder och/eller specifik hantering av Adobe kan Adobe behålla vissa anpassade egenskaper för varje Pay TV-leverantör. Dessa operatorspecifika konfigurationer/principer inkluderar aktivering av fördefinierade arbetsflöden som kan startas vid specifika punkter i arbetsflödet på den översta nivån. Kontakta din Adobe-representant om du vill ha mer information om stöd för anpassade egenskaper.

Adobe erbjuder också bedrägeribegränsande tjänster. Kontakta din Adobe-representant för mer information.

### Programmeringsprocessen {#programmer-process}

För att Adobe Primetime-autentisering ska fungera måste programmerarna konfigurera sina mediespelarprogram eller webbsidor så att de kan arbeta med Adobe Primetime-autentisering när de hanterar de viktigaste tillståndsprocesserna: autentisering, auktorisering och utloggning.


Innan en integrering med Adobe Primetime-autentisering påbörjas bör programmerarna ha:

* En befintlig videoplattform online, inklusive en mediespelare, antingen som en del av en webbplats eller som ett fristående program
* Ett innehållshanteringssystem
* En leveransmekanism som kan omfatta ett leveransnätverk från tredje part (CDN)

Programmerarna kan förvänta sig att få utföra vissa integreringsuppgifter som en del av att tillhandahålla TV Everywhere-tjänster med Adobe Primetime-autentisering. Bland dessa uppgifter finns:

* Integrera Adobe Primetime-autentiserings Access Enabler-bibliotek i din webbsida eller mediespelare, eller implementera integrering med hjälp av metoden Klientlös för&quot;smarta enheter&quot; som inte är webbkompatibla
* Arbete på serversidan för att integrera verifieringskomponenten för Adobe Primetime-autentiseringstoken i arbetsflödet för videoströmning
* Skapa ett användargränssnitt för arbetsflödet till din webbplats eller app (vissa element i det, till exempel den faktiska inloggningsprocessen, tillhandahålls av Pay TV-operatören och vissa element är eventuellt tillgängliga som en del av Adobe Primetime-autentiseringen)

Rapporten ger en översikt över Programmeringsprocessen och Adobe ger ytterligare vägledning när integreringen formellt påbörjas.

#### Installationsprogram för begärande (programmerare) {#requester-prog-setup}

##### Registrering hos Adobe {#registering}

Som ett första steg måste programmerare registrera sig hos Adobe eller en Adobe-auktoriserad partner och ange vilka domäner de vill använda med Adobe Primetime-autentisering. Programmerarna får sedan ett unikt begärande-ID som skickas till Adobe Primetime-autentiseringen för varje session där Programmeraren interagerar med Access Enabler.

##### Inställning för integrering av första åtkomstaktivering {#access-enabler-int-setup}

Programmerarna måste integrera klientkomponenten för Adobe Primetime-autentisering, Access Enabler, i sina befintliga mediespelarappar eller webbsidor innan de kan begära åtkomst till innehåll. Det finns olika alternativ för att göra detta:

* Du kan bädda in Flashen AccessEnabler.swf, i en videospelare som är baserad på Flashar på en webbsida eller direkt i HTML. Du kan kommunicera med SWF i ActionScriptet eller JavaScript. Bas-API:t är ActionScript, men ett fullständigt JavaScript-bibliotek finns tillgängligt.
* För enheter som inte är Flashar kan du:
   * Använd HTML5-/JavaScript-versionen, AccessEnabler.js, och kommunicera med den via JavaScript-API:t, eller
   * Använd ett systemspecifikt Access Enabler-bibliotek, t.ex. för iOS, Android eller Windows 8

##### Inställning för inledande API-integrering utan klient {#clientless-api-int-setup}

Innan kunder som begär åtkomst till innehåll kan begära att programmerare implementerar RESTful-webbtjänstanrop med hjälp av klientlöst API i sin mediespelarapp, samt ställer in ett&quot;sekundärt skärmsprogram&quot; för att hantera användarens inloggning på sin Pay TV-leverantör via webben.

#### Hantera autentisering och auktorisering {#auth-authr-handling}

När en kund begär en skyddad resurs från en programmerare för första gången, visar programmeraren kunden en lista över vilka leverantörer av betal-TV som de kan välja mellan. När providern är vald omdirigeras användaren till den operatorn för inledande användarautentisering. När autentiseringen är klar kommunicerar Adobe Primetime-autentiseringen med den valda Pay TV-leverantören för att auktorisera åtkomst till den angivna resursen. Information om dessa processer följer.

![](assets/providr-selection-ui.png)


*Figur 3: Exempel på användargränssnitt för val av leverantör*

>[!NOTE]
>
>* Autentisering sker som ett SAML-utbyte mellan Adobe Primetime-autentisering som tjänsteleverantör (eller SP) och en Pay TV-leverantör som identitetsleverantör (eller IdP).
>* Auktoriseringen använder ett serverbaserat webbtjänstutbyte (server-till-server) mellan Adobe Primetime-autentisering (SP) och en Pay TV-leverantör (IdP).


##### Programmeringskommunikation med hjälp av åtkomstfunktionen

Den tvåvägskommunikationskanal som finns mellan Access Enabler och programmerarens webbsida eller spelarapp följer ett fullständigt asynkront mönster. Programmeraren skickar meddelanden till Access Enabler via de metoder som finns i API:t för Access Enabler. Access Enabler svarar via återanrop som är registrerade i Access Enabler-biblioteket.

* Alla auktoriseringsbegäranden begär automatiskt autentisering först, om det inte finns någon autentiseringstoken på det lokala systemet. När autentiseringen lyckas lagras kundens token lokalt, så att de inte behöver logga in igen under en viss tidsperiod. Om de har autentiserats med Adobe Primetime autentiseringsberättigande i något annat sammanhang (t.ex. via Pay TV-leverantörens webbplats eller en annan programmerare) har Access Enabler åtkomst till den lokala token och kräver ingen ytterligare autentisering.
* När en kund begär en viss resurs begär programmeraren tillstånd från Pay TV-leverantören via Access Enabler. Efter verifiering (eller initiering) av autentiseringen kontaktar Access Enabler leverantören av betal-TV (via Adobe Primetime-autentisering) för att avgöra om kunden har rätt att se resursen. Adobe Primetime-autentisering hanterar kommunikation med Pay TV-leverantören för att få behörighet. Programmeraren behöver bara skicka begäran till Access Enabler och hantera svaret (om auktoriseringen lyckades eller misslyckades). Om auktoriseringen lyckas lagras en auktoriseringstoken på klientdatorn och återanropet tar emot en kort medietoken.

##### Programmeringskommunikation med API:t för klientlösa {#progr-comm-clientless-api}

Kommunikation mellan Programmerarens app och Adobe Primetime-autentisering sker via RESTful-webbtjänster.  Det finns säkerhetsprotokoll för alla API-anrop till slutpunkterna för Adobe Primetime-autentisering.  Säkerhetskrav beskrivs i dokumentationen för klientlöst API.

##### Exempel på arbetsflöde med SAML Web Browser SSO-baserad autentisering {#sample-wf}

1. Visningsprogrammet navigerar till en webbplats (dummy1.com) och försöker få åtkomst till det berättigade innehållet.
1. Videosida/spelare läser in åtkomstaktiveraren från adobe.com och frågar efter auktorisering för det begärda innehållet när användaren uppmanas att göra det.
1. Access Enabler kör och validerar den som gjorde begäran och begäran.
1. Åtkomstaktivering söker efter en giltig auktoriseringstoken i lokal butik. Om en giltig auktorisering hittas skapar Access Enabler en kort medietoken (se steg 14).
1. Om ingen giltig auktorisering för den begärda resursen hittas men det finns en giltig autentiseringstoken, initierar Access Enabler en auktoriseringsbegäran med Pay TV-leverantören om att användaren autentiseras mot den. Adobe-servern tillhandahåller auktoriseringsförfrågan/svarsutbyte med Pay TV-leverantören.
1. Om ingen giltig autentiseringstoken hittas uppmanas användaren att ange sin leverantör av betal-TV. (Om du väljer en provider som stöder SSO-baserad autentisering i SAML-webbläsaren aktiveras ett SAML-baserat autentiseringsarbetsflöde. För icke-SAML-providers hanterar Adobe ett liknande anpassat arbetsflöde.)
1. Access Enabler navigerar webbläsaren till tjänsten Adobe SAML SP (tjänsteleverantör) och skickar den med alla lämpliga parametrar.
1. SAML SP anropar rätt SAML IdP (Identity Provider) hos användarens Pay TV-leverantör med hjälp av SAML-webbläsarprofilen som anges i IdP-metadata. På så sätt navigerar användaren till webbplatsen för IdP:er (Pay TV provider), där användaren autentiserar.
1. När autentiseringen är klar omdirigeras användaren tillbaka till Adobe SAML SP och skickar ett autentiserings-GUID i SAML-svaret.
1. Adobe SAML SP skapar en session på serversidan där autentiserings-GUID lagras och dirigerar om användaren tillbaka till den ursprungliga programmerarsidan. (Serversessionen tas bort när åtkomstaktiveraren hämtar authN-token.)
1. Åtkomstaktivering hämtar autentiserings-GUID från Adobe-servern som ska ingå i token med ett enhets-ID som upprätthålls av Adobe Primetime-autentisering. När Flash-DRM finns på enheten görs detta via Flash Access-API:er (Flashens Player DRM-komponent) som möjliggör bindning av GUID till enhets-ID och returnerar en autentiseringstoken. I annat fall görs detta via JS-API:er via HTTPS med HTML5-baserad lagring eller via specifika systemkomponenter.
1. Autentiseringstoken används av Access Enabler för att göra auktoriseringsbegäranden till Pay TV-leverantören. På enheter som har stöd för Flash Access görs förfrågningarna alltid via Flash Access-API:er så att den auktoriseringstoken som skapas binds till enheten. På enheter som inte är Flashar Access används HTTPS för säker kommunikation från klient till server.
1. När auktoriseringen är klar skapar Adobe Primetime-autentiseringen en token för långvarig auktorisering (&quot;authZ&quot;) och skickar den till Access Enabler, som lagrar den på det lokala systemet.
1. Åtkomstaktiveraren använder authZ-token för att skapa kortlivade medietoken som används för visningsåtkomst. Av säkerhetsskäl måste dessa kortlivade token valideras av en annan Adobe Primetime-autentiseringskomponent, Media Token Verifier.

![](assets/authn-authz-entitlmnt-flow.png)


*Bild 4: Arbetsflöde för aktivering av autentisering och auktoriseringsåtkomst*

##### Ange ett berättigandeanvändargränssnitt {#entitlement-ui}

Programmerarna måste skapa ett eget användargränssnitt för att få tillgång till arbetsflödet på sin webbplats eller i sin app. Vissa element, till exempel den faktiska inloggningsprocessen, tillhandahålls av Pay TV-leverantören och vissa element är eventuellt tillgängliga som en del av Adobe Primetime-autentiseringen. Programmeraren utför minst följande:

* **Implementerar ett gränssnitt för val av leverantör** som gör att en ny användare kan identifiera sin Pay TV-leverantör och logga in för första gången. För utveckling har Access Enabler ett grundläggande användargränssnitt som ger kunden möjlighet att välja mellan leverantörer av betal-TV och som initierar inloggningsprocessen. I en produktionsmiljö måste programmerarna implementera en egen dialogruta för leverantörsväljare. Vissa leverantörer av betal-TV dirigerar om sig till sin egen webbplats för inloggning, och vissa kräver att deras inloggningssidor visas i en iframe. Programmerarna måste implementera det återanrop som skapar den här iframe-versionen om kunden väljer någon av dessa leverantörer.
* **Identifierar skyddade resurser.** Skyddade resurser är sådana som kräver åtkomstbehörighet. När du erbjuder dessa resurser bör programmeringsgränssnittet ange att det behövs behörighet innan du kan titta på dem. När auktoriseringen är klar bör gränssnittet visa att resursen nu är auktoriserad.
* **Skapar och underhåller en lista över leverantörer av betal-TV** för att styra användaråtkomst till endast de leverantörer som du anger.
* **Visar att en användare är autentiserad.** Programmeraren ska ange kundens autentiseringsstatus som en del av det sätt som används för att identifiera skyddade resurser. Programmerarna kan fråga Access Enabler för att avgöra om en kund redan har autentiserats.

#### Stöd för enkel utloggning {#single-logout-support}

I de flesta fall ansvarar programmeraren för att hantera användarutloggningar via ett enkelt API-anrop. Anropet logOut() instruerar Primetime-autentisering att logga ut den aktuella användaren genom att:

* Tar bort alla AuthN- och AuthZ-token
* Rensa all autentiserings- och auktoriseringsinformation för den användaren
* Initierar ett arbetsflöde som är specifikt för en Pay TV-leverantör för att rensa bort användarens autentiseringssession med leverantören (om autentiseringen till exempel gjordes med protokollet SAML Authentication Request, kan utloggningen göras med protokollet SAML Single Logout.)

Om användaren lämnar datorn inaktiv tillräckligt länge så att deras tokens går ut, kan de fortfarande återgå till sin session och initiera utloggningen. Adobe Primetime-autentisering säkerställer att alla tokens tas bort och meddelar Pay TV-leverantören att även ta bort deras session.


När utloggningen initieras från en webbplats som inte är integrerad med Adobe Primetime-autentisering kan betal-TV-leverantören anropa Adobe Primetime-tjänsten för autentisering av enkel utloggning via en webbläsaromdirigering.

## Utöver de grundläggande berättigandeflödena - ytterligare funktioner {#beyond-basics}

De grundläggande tillståndsflödena är Start, Autentisering, Autentisering och Logout.  När Adobe Primetime-autentiseringen mognar och utvecklas har ett antal ytterligare funktioner lagts till i basflödena.  Bland dessa finns:

* **Användarmetadata** - Beroende på avtal mellan programmerare och distributörer kan programmerare på ett säkert sätt utbyta metadata som Zipcode, maximum rating, channel ID med mera. Metadata möjliggör olika användningsområden, t.ex. föräldrakontroll, regionala frysperioder för idrottsevenemang m.m.
* **Tillfällig kostnadsfri åtkomst** - Programmerarna kan tillfälligt få fri tillgång till sitt skyddade innehåll (t.ex. korta prov av daglig programmering eller kostnadsfri presentation av ett stort evenemang).
* **Proxy MVPD** - Ett MVPD-program kan hantera sin egen integrering med Adobe Primetime-autentisering och även hantera tillståndsprocessen för en grupp av associerade ProxiedMVPD-program.

## Säkerhet {#security}

I det här avsnittet beskrivs säkerheten och integriteten för Adobe Primetime autentiseringsinfrastruktur.

### Tokensäkerhet {#token-security}

Ett av de främsta målen med Adobe Primetime-autentisering är att se till att systemet klarar att angripa innehållsberättigandedata av en obehörig användare eller innehållsaggregator. Därför skyddas dataåtkomsten på olika nivåer i arbetsflödet, vilket skyddar genereringen och användningen av autentiseringstokendata som har störst betydelse. Adobe Primetime autentiseringsarkitektur är utformad för att säkerställa att tokeninnehållet upprätthålls på ett säkert sätt och att token finns kvar på den enhet som den utfärdades till.

* **Långvarig AuthN- och AuthZ-tokensäkerhet** - Alla långvariga token signeras digitalt av Adobe Primetime autentiseringsserver. Den digitala signaturen skiljer sig dock från plattform till plattform eftersom den använder ett enhets-ID som skiljer sig åt när det gäller hur det genereras, skyddas och valideras. I samtliga fall säkerställer en validering på klientsidan att den digitala signaturen är intakt och att token-integriteten bevaras. Åtkomstaktiveraren lagrar de validerade tokenerna säkert på platser som är specifika för den miljö där den körs. Om validering av enhets-ID misslyckas ogiltigförklaras autentiseringssessionen, tokens återställs och användaren uppmanas att logga in igen.
* **Kortlivad säkerhet för medietoken** - Kortlivade medietokens, som produceras i det sista steget före innehållsåtkomst, signeras av Adobe och krypteras för att undvika manipulering under utbyte. Kortlivade medietoken kräver också ett extra valideringssteg av ytterligare en autentiseringskomponent från Adobe Primetime, Media Token Verifier. TTL för den kortlivade token är inställd på 5 minuter och kan göras kortare om så önskas. Den kortlivade medietoken cachelagras aldrig. En ny token hämtas från servern varje gång ett auktoriserings-API anropas.

### Plattformsspecifik enhetssäkerhet {#platform-sp-security}

Vilka säkerhetsåtgärder som används vid Adobe Primetime-autentisering varierar beroende på plattform, men alla är robusta och av allra högsta klass.

* **Enheter med Flash** - När Flash Player 10.1+ eller AIR 2.5+ finns på enheten använder Adobe Primetime-autentiseringen Flashens Player DRM-funktion för skydd, som också kallas Flash Access. Flash ger en extra skyddsnivå. Den starka säkerheten för enhetsbindning för Flash-baserade tokens innebär i de flesta fall att time-to-live kan vara längre, att  inte behöver logga in lika ofta och att användarupplevelsen i allmänhet är smidigare.
* **Webbläsarupplevelser på enheter med HTML5-funktioner**- På enheter som inte är Flashar och som har webbläsarfunktioner i HTML5 har Adobe Primetime-autentisering ett alternativt sätt att begränsa skyddet för webbläsarbaserade integreringar. Men eftersom enhetsbindningen för HTML5 inte är lika stark är TTL (time-to-live) för token på HTML5-plattformar vanligtvis kortare.
* **Inbyggt stöd för enheter hemma och utanför** - Adobe erbjuder systemspecifika SDK per operativsystem (iOS, Android, Windows 8 osv.) som ger ökad säkerhet över HTML 5-lösningen. Dessa SDK:er använder inbyggda API:er för att hämta ett enhets-ID och skicka det säkert till Adobe Primetime autentiseringsserver.
* **Klientlös** - Adobe Primetime-autentisering använder HTTPS-protokollet för säker kommunikation. Dessutom måste alla samtal från en smart enhet signeras digitalt.

## Vanliga frågor {#faqs}

**Vad är TV Everywhere?**
Branschrörelsen TV Everywhere gör det möjligt för betal-TV-kunder att få tillgång till det premiuminnehåll de redan prenumererar på på en mängd olika internetanslutna enheter, inklusive persondatorer, surfplattor, smarttelefoner, spelkonsoler, digitalboxar och&quot;smarta&quot; tv:er. Utmaningen med det här initiativet är att göra autentiseringsprocessen så enkel och smidig som möjligt, så att kunderna smidigt kan komma åt sitt prenumerationsmaterial utan hinder och flera inloggningar.


**Vad är Adobe Primetime-autentisering och hur hör den ihop med TV Everywhere?**
Adobe Primetime-autentisering tar TV Everywhere från koncept till verklighet genom att smidigt verifiera användarens rätt till innehåll på ett sätt som är både enkelt och säkert. Adobe Primetime autentisering är en värdtjänst som möjliggör snabb backend-integrering baserat på de affärsregler som krävs av både programmerare och betal-TV-leverantörer. Detta innebär en snabb time to market för alla parter, en säkrare miljö för att förhindra bedrägerier och en överlägsen kundupplevelse, med mer TV-innehåll tillgängligt för fler personer över flera plattformar.


**Hur erbjuds/levereras Adobe Primetime-autentisering?**
Adobe Primetime autentisering erbjuds via SaaS-modellen (Software as a Service). Detta gör det möjligt att kommunicera säkrare mellan slutanvändare, programmerare och betal-TV-leverantörer för att validera rätten till innehåll. Huvudkomponenterna i tjänsten är klientåtkomstaktivering (eller klientlöst API för vissa enheter) och värdbaserad Adobe Primetime-autentiseringsserver. Access Enabler är en liten fil som läses in i programmerarens webbsida eller spelarprogram. Den kommunicerar med Adobe Primetime autentiseringsservrar, som i sin tur har anslutningar inbyggda i autentiseringssystemen hos olika Pay TV-leverantörer. Adobe Primetime-autentisering erbjuder även en klientlös API-metod för integrering av vissa&quot;smarta enheter&quot; som inte är webbkompatibla (smarta TV-apparater, digitalboxar, spelkonsoler osv.). Klientlösa metoder tillhandahåller RESTful-webbtjänster som utvecklare kan använda för att implementera Adobe Primetime autentiseringstillståndsflöden på dessa enheter.


**Hur skiljer sig Adobe Primetime autentisering från andra TV Everywhere-lösningar?**
Adobe Primetime autentisering har tydliga fördelar jämfört med alternativa TV Everywhere-lösningar. Direkt integrering med enskilda leverantörer ger inte flexibilitet med en enda, beständig inloggning (SSO) när användare reser från webbplats till webbplats över Internet. Adobe Primetime autentisering har också en anmärkningsvärd genomslagskraft på marknaden. När en programmerare har integrerats med Adobe Primetime-autentisering är de omedelbart anslutna till Pay TV-operatörer som betjänar över 90 % av hushållen i USA. Dessutom utnyttjar Adobe Primetime-autentisering unika säkerhetsfunktioner som är inbyggda i Flash runtime (där de är tillgängliga) för att minska risken för bedrägeri, samtidigt som SDK:er tillhandahålls så att programmerare kan ha samma TV Everywhere-funktionalitet inbyggda i inbyggda appar för mobiler och hemenheter där Flash inte är tillgänglig. Slutligen, medan Adobe Primetime autentisering är tillgänglig som en fristående tjänst erbjuder vi också möjligheten att ha nära integrering med andra Adobe-produkter och -tjänster (inklusive Primetime och Adobe Analytics) som rör leverans, skydd och intäktsgenerering av TV Everywhere-innehåll.

**Hur säker är Adobe Primetime autentisering?**
Den främsta prioriteten med Adobe Primetime autentiseringsarkitektur är att säkerställa att endast behöriga tittare autentiseras och beviljas åtkomst till premiuminnehåll. Adobe Primetime autentisering binder åtkomsten till visningsenheten och kan bidra till att begränsa strömmar, sessioner och/eller enheter för ett visst hushåll.


**Krävs Flash Player?**
Adobe Flash Player 11.x eller senare krävs för den striktaste enhetsbindningssäkerheten. Adobe Primetime autentisering för TV Everywhere är dock en spelare och plattformsoberoende som integreras med alla uppspelningsprogram, inklusive Silverlight och HTML5. Dessutom ger Adobe Primetime-autentisering inbyggt stöd för enheter som iOS, Android och Xbox där Flash Player inte är tillgänglig.  Adobe Primetime-autentisering är slutligen en klientlös metod för enheter som inte kan återge webbsidor (spelkonsoler, smarta TV-apparater, digitalboxar).


**Vilka enheter stöder Adobe Primetime autentisering?**
Adobe Primetime-autentisering stöds av praktiskt taget alla enheter med webbpaketet HTML5 för visning i webbläsare. Dessutom fortsätter Adobe Primetime-autentisering att lansera SDK:er (native software development kit) för olika enhetsspecifika plattformar som iOS, Android™ och Windows 8. Adobe Primetime-autentisering stöder delvis vissa enheter som inte är webbkompatibla (smarta TV-apparater, digitalboxar, spelkonsoler osv.) genom sina RESTful web services API:er.

**Har Adobe Primetime autentisering stöd för de nya standarderna för TV Everywhere?**
Adobe Primetime-autentisering är kompatibel med **CableLabs OLCA (Online Content Access)** [specifikation](https://www.cablelabs.com/specifications), som innehåller tekniska krav och arkitektur för leverans av video till en Pay TV-kund från onlinekällor. Adobe deltog i det gemensamma CableLabs-projektet för interopt-testning i juni 2011 och klarade testprocessen för en implementering av en tjänsteleverantör. Adobe Primetime-autentisering verifieras (slutförd och testad) mot OLCA-specifikationerna för autentisering. Auktoriseringskomponenten är slutförd, men testverifieringen väntar på att testmiljön för CableLabs ska släppas (ETA Nov 2011).

Adobe är även aktiv medlem i **OATC (Open Authentication Technical Consortium)** och deltar i flera av underkommittéernas projekt för att utarbeta specifikationer som en del av det organet.

**Hur hanterar Adobe Primetime-autentisering federerad identitetshantering/enkel inloggning (SSO)?**
Med Adobe Primetime-autentisering kan du ge kunderna autentisering och auktorisering med enkel inloggning (SSO) genom att använda bakkanalskommunikation (server-till-server) mellan Adobe Primetime-autentisering och deltagande Pay TV-operatörer. Med Adobe Primetime-autentisering behöver abonnenterna inte logga in igen efter den första autentiseringen, så länge som autentiseringen tillåts av Pay TV-operatören. Den här gränsen är vanligtvis 30 dagar. För att uppnå detta tillhandahåller Adobe Primetime-autentisering en gemensam domän för autentiseringstoken för våra kunder. Den här autentiseringstillståndsinformationen är tillgänglig för alla deltagande webbplatser som är integrerade med en viss Pay TV-operatör.

För närvarande använder de flesta av Adobe Primetime autentiseringsintegreringar med Pay TV-operatörer SAML-protokollet, en av de primära autentiseringsstandarderna. Adobe Primetime-autentisering fungerar som proxytjänsteleverantör i SAML-arkitekturen och behåller SAML-autentiseringssvaret som en säker token i den gemensamma domänen Adobe. Adobe Primetime-autentisering är SAML 2.0-kompatibel.

Adobe Primetime-autentisering används vanligtvis med SAML SSO-lösningar i nuläget, men Adobe Primetime autentiseringsarkitektur tar bort alla protokollspecifika delar från programmerarintegreringen. Därför kan stöd för nya protokoll, t.ex. ett som är baserat på OAuth 2.0 eller anpassade protokoll, läggas till över tiden.

**Vad kostar Adobe Primetime-autentisering för TV Everywhere för slutanvändarna?**
Slutanvändarna behöver inte betala någon extra kostnad för att använda Adobe Primetime-autentisering.

>[!NOTE]
>
>**Nästa steg:** Kontakta Adobe eller fyll i formuläret för begäran om information om du vill ha mer information [här](https://www.adobe.com/cfusion/mmform/index.cfm?name=adobepass_rfi).
>
