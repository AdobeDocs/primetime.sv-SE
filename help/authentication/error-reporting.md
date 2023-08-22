---
title: Felrapportering
description: Felrapportering
exl-id: a52bd2cf-c712-40a2-a25e-7d9560b46ba6
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# Felrapportering {#error-reporting}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.


## Ökning {#overview}

Felrapportering i Adobe Primetime-autentisering är för närvarande implementerat på två olika sätt:

* **Avancerad felrapportering** Implementeraren registrerar ett felanrop om [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk) eller implementerar en gränssnittsmetod med namnet &quot;`status`&quot; om [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk) och [AccessEnabler Android SDK](#accessenabler-android-sdk)för att få avancerad felrapportering. Fel kategoriseras i **Information**, **Varning** och **Fel** typer. Det här rapporteringssystemet är **asynkron** i den **det inte finns någon garanti för i vilken ordning flera fel kommer att utlösas**.  Mer information om det avancerade felrapporteringssystemet finns i [Avancerad felrapportering](#advanced-error-reporting) -avsnitt.

* **Ursprunglig felrapportering -** Ett statiskt rapporteringssystem där felmeddelanden skickas till specifika callback-funktioner när specifika begäranden misslyckas. Fel grupperas i generiska, autentiserings- och auktoriseringstyper. En lista över fel som rapporterats i det ursprungliga systemet finns i [Ursprunglig felrapportering](#original-error-reporting) -avsnitt.


## Avancerad felrapportering {#advanced-error-reporting}

* [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk)
* [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk)
* [AccessEnabler Android SDK](#accessenabler-android-sdk)
* [AccessEnabler FireOS SDK](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>Den gamla [Ursprunglig felrapportering](#original-error-reporting) API kommer att fortsätta fungera som tidigare, den avancerade felrapporteringen bryter inte funktionen, men den ursprungliga felrapporteringen kommer INTE att få några uppdateringar längre. Alla nya fel och uppdateringar kommer att inträffa i det avancerade felrapporteringssystemet.

### AccessEnabler JavaScript SDK {#accessenabler-javascript-sdk}

Det nya felrapporteringssystemet är inte obligatoriskt, och därför kan implementeraren uttryckligen registrera ett felhanteringsanrop för att få avancerade felrapporter. I systemet kan du registrera och avregistrera flera felåteranrop dynamiskt. Dessutom kan du registrera nya felåteranrop så snart AccessEnabler JavaScript SDK har lästs in, utan att någon annan initiering behöver utföras (innan du anropar `setRequestor()`), vilket innebär att du kan ta emot avancerade rapporter om initierings- och konfigurationsfel.


#### Implementering {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


Callback-funktionen för felhanteraren får ett enda objekt (en karta) med följande struktur:

```JavaScript
    {
      errorId: "CFG410",
      level: "error",
      message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

### 1. Bind {#bind}

**`.bind(eventType:String, handlerName:String):void`**

Kopplar en hanterare för en händelse.

**`eventType`** - ENDAST &quot;`errorEvent`&quot; resulterar i att AccessEnabler JavaScript SDK utlöser avancerade felrapporter för återanrop.

**`handlerName`** - en sträng som anger namnet på felhanterarfunktionen.


Båda bind-parametrarna får endast innehålla tecken från följande uppsättning: `[0-9a-zA-Z][-._a-zA-Z0-9]`; det vill säga, parametrar måste börja med en siffra eller bokstav och kan sedan bara innehålla bindestreck, punkter, understreck och alfanumeriska tecken.  Dessutom får parametrarna inte överskrida 1 024 tecken.

**Exempel** för felhanterare för bindning:

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

På grund av tekniska begränsningar kan du inte binda ett stängningsställe eller en anonym funktion. Du måste ange metodens namn i den andra parametern.


### 2. Lås upp bindning {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

Tar bort en tidigare kopplad händelsehanterare.

**`eventType`** - ENDAST &quot;`errorEvent`&#39; resulterar i att JavaScript SDK för AccessEnabler utlöser avancerade felrapporter.

**`handlerName`** - en sträng som anger namnet på felhanterarfunktionen, om är null eller saknar alla kopplade hanterare för den angivna `eventType` tas bort.

Båda bind-parametrarna får endast innehålla tecken från följande uppsättning: `[0-9a-zA-Z][-._a-zA-Z0-9]`; det vill säga, parametrar måste börja med en siffra eller bokstav och kan sedan bara innehålla bindestreck, punkter, understreck och alfanumeriska tecken.  Dessutom får parametrarna inte överskrida 1 024 tecken.

**Exempel** för att ta bort en enda felhanterare:

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**Exempel** ta bort alla felhanterare:

`accessEnabler.unbind('errorEvent');`


### AccessEnabler iOS/tvOS SDK {#accessenabler-ios-tvos-sdk}

Det nya felrapporteringssystemet är obligatoriskt, och därför måste den som genomför felrapporteringen uttryckligen följa det nya mål C-protokollet &quot;EntitlementStatus&quot;. Med den här nya metoden kan programmerare få avancerad felrapportering.

#### Implementering {#accessenab-ios-tvossdk-imp}

En implementator måste uppfylla följande **EntitlementStatus** protokoll:

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

Dina **status** -funktionen tar emot ett enda objekt (en `NSDictionary`) med följande struktur:

```OBJ-C
    {
          errorId: "CFG410",
          level: "error",
          message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

**1. Deklaration**

```OBJ-C
    @interface MyEntitlementStatusDelegate : NSObject <EntitlementStatus>
```

**2. Implementering**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### AccessEnabler Android SDK {#accessenabler-android-sdk}

Det nya felrapporteringssystemet är obligatoriskt eftersom implementeraren måste följa `IAccessEnablerDelegate` gränssnittsdefinierat protokoll. Med den här nya metoden kan programmerare få avancerad felrapportering.

#### Implementering {#access-enablr-androidsdk-imp}

En utvecklare måste kunna hantera det nya `status` metod från gränssnittet`IAccessEnablerDelegate`. The **`status`** funktionen får en **`AdvancedStatus`** objekt med följande modell:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Exempel**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

### AccessEnabler FireOS SDK {#accessenabler-fireos-sdk}


Det nya felrapporteringssystemet är obligatoriskt eftersom implementeraren måste följa `IAccessEnablerDelegate` gränssnittsdefinierat protokoll. Med den här nya metoden kan programmerare få avancerad felrapportering.

#### Implementering {#access-enab-fireos-sdk-}

En utvecklare måste kunna hantera det nya `status`metod från gränssnittet`IAccessEnablerDelegate`. The **`status`** funktionen får en **`AdvancedStatus`** objekt med följande modell:

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**Exempel**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

## Avancerad felkodsreferens {#advanced-error-codes-reference}

I följande tabell visas och beskrivs felkoderna som visas av det nyare fel-API:t, tillsammans med förslag på åtgärder som ska vidtas för att korrigera dem:

| ID | Nivå | Beskrivning | Utvecklaråtgärder | Användaråtgärder | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL &amp; AAPL_ERROR | Fel | Allmänt Apple SSO-fel | Felet innehåller ett informationsfält med det ursprungliga VSA-felet. | n/a | n/a | Ja | n/a |
| VSA203 | Info | Användaren bestämde sig för att logga ut från programmet medan autentiseringen gjordes som ett resultat av en inloggning via plattformens SSO. | Instruera/uppmana användaren att explicit logga ut från Inställningar -> Konton -> TV-leverantör på tvOS. <br><br> Instruera/uppmana användaren att explicit logga ut från Inställningar -> TV-leverantör på iOS/iPadOS. | Logga ut explicit från Inställningar -> Konton -> TV-leverantör på tvOS. <br> <br> Logga ut explicit från Inställningar -> TV-leverantör på iOS/iPadOS | n/a | Ja | n/a |
| VSA404 | Info | Behörigheten för programvideoprenumerantkontot är inte fastställd. | Uppmuntra användare som vägrar ge behörighet att få åtkomst till prenumerationsinformation genom att förklara fördelarna med SSO (Single Sign-On). | Användaren kan ändra sitt beslut genom att gå till programinställningarna (tv-leverantörsåtkomst) eller till avsnittet Inställningar -> TV-leverantör på iOS/iPadOS eller Inställningar -> Konton -> TV-leverantör på tvOS. | n/a | Ja | n/a |
| VSA503 | Info | Metadatabegäran för Application Video Subscriber Account misslyckades. | MVPD-slutpunkten svarar inte. Programmet kan återgå till det reguljära autentiseringsflödet. | n/a | n/a | Ja | n/a |
| 500 | Fel | Internt fel | Använd AccessEnablerDebug och inspektera felsökningsloggar (console.log output) för att avgöra vad som gick fel. | n/a | Ja | Ja | n/a |
| SEC403 | Fel | Domänsäkerhetsfel. Den som gjorde begäran använder en ogiltig domän. Alla domäner som används av ett visst begärande-ID måste vitlistas av Adobe. | - Läs bara in AccessEnabler från listan över tillåtna domäner <br> <br> - Kontakta Adobe för att hantera domänens vitlista för det begärande-ID som används <br> <br> - iOS: verifiera att du använder rätt certifikat och att signaturen har skapats korrekt | n/a | n/a | Ja | n/a |
| SEC412 | Varning | [Finns i version 2.5] Enhets-ID matchar inte. Detta kan inträffa när den underliggande plattformen ändrar sitt enhets-ID. I det här fallet kommer de befintliga tokenerna att rensas och användaren kommer inte att autentiseras längre. Observera att detta sker lagenligt när användaren använder JS SDK och roaming (på JS är klientens IP-adress en del av enhets-ID). I annat fall kan detta vara en indikation på ett försök att kopiera tokens från en annan enhet. | - Övervaka antalet varningar. Om de kraschar utan någon uppenbar anledning (inga nya webbläsaruppdateringar eller nya operativsystem) som kan vara en indikator på försök till bedrägeri.  <br> <br>- Du kan även informera användaren om att han/hon måste logga in igen. | Logga in igen. | Ja | Ja | Ja från 3.2 |
| SEC420 | Fel | HTTP-säkerhetsfel vid kommunikation med Adobe Primetime autentiseringsservrar. Det här felet inträffar vanligtvis när det finns förfalskningar eller utkast. | - Läs in `[https://]{SP_FQDN\}` i webbläsaren och acceptera SSL-certifikaten manuellt, till exempel **https://api.auth.adobe.com** eller **https://api.auth-staging.adobe.com** <br> <br>- Markera proxycertifikaten som tillförlitliga | Om detta inträffar för en vanlig användare är det en indikation på en möjlig man-in-the-middle-attack! | Ja | Ja | Ja från 3.2 |
| CFG100 | Varning | Klientdatorns datum/tid/tidszon är inte korrekt inställd. Detta leder troligtvis till autentiserings-/auktoriseringsfel. | - Informera användaren om att ställa in rätt tid. <br> <br> Vidta åtgärder för att förhindra tillståndsflöden, eftersom de troligtvis kommer att misslyckas. | Ange korrekt datum/tid. | Ja | Ja | Ja från 3.2 |
| CFG400 | Fel | Ett ogiltigt begärande-ID angavs. | Utvecklaren MÅSTE ange ett giltigt begärande-ID. | n/a | Ja | Ja | Ja från 3.2 |
| CFG404 | Fel | Det gick inte att hitta Adobe Primetime autentiseringsservrar. Detta kan inträffa i 3 instanser: <br><br> - Utvecklaren har en ogiltig förfalskning. <br><br> -Användaren har nätverksproblem och kan inte nå Adobe Primetime autentiseringsdomäner. <br><br> -Adobe Primetime autentiseringsservrar är felkonfigurerade. <br><br>  **Obs!** I Firefox visas CFG400 i stället för CFG404 (webbläsarbegränsning) | - Kontrollera spoofing. <br><br> -Kontrollera nätverks-/DNS-inställningar. <br><br> -Inform Adobe. | Kontrollera nätverks-/DNS-inställningar. | Ja | Ja | Ja från 3.2 |
| CFG410 | Fel | AccessEnabler är för gammal. | Informera användaren om att rensa cacheminnen. | Rensa webbläsarcachen. | Ja | n/a | Ja från 3.2 |
| CFG5xx | Fel | Adobe Primetime autentiseringsservrar har interna fel. xx kan vara vilket tal som helst. | - Informera användaren om att Adobe Primetime-autentisering inte är tillgänglig. <br><br> - Kringgå Adobe Primetime-autentisering. <br> <br> - Informera Adobe. | Försök senare. | Ja | Ja | Ja från 3.2 |
| N000 | Info | Användaren är inte autentiserad. | n/a | Logga in. | Ja | Ja | Ja från 3.2 |
| N001 | Info | Ett passivt autentiseringsförsök startades i bakgrunden. Detta inträffar för MVPD-program som konfigurerats med &quot;Authentication Per Requestor&quot;. Användaren autentiseras förhoppningsvis automatiskt, men detta medför prestandaförluster vid initieringen. | Du kan också informera användaren, eller presentera användargränssnittet som varnar användaren, om att&quot;arbetet pågår&quot;. | Vänta. | Ja | Ja | Ja från 3.2 |
| N003 | Info | Användaren väljer alternativet &quot;Annan TV-leverantör&quot; i Apple MVPD-väljaren. | The *displayProviderDialog* återanrop anropas och programmet kan återställas till det reguljära autentiseringsflödet. | Välj vanlig MVPD och fortsätt med inloggningsskärmen. | n/a | Ja | n/a |
| N004 | Info | Användaren väljer en tv-leverantör som inte stöds av den aktuella begäraren. | The *displayProviderDialog* återanrop anropas och programmet kan återställas till det reguljära autentiseringsflödet. | Välj vanlig MVPD och fortsätt med inloggningsskärmen. | n/a | Ja | n/a |
| N005 | Info | MVPD-väljaren avbröts. | n/a | n/a | Ja | Ja | Ja från 3.2 |
| N010 | Varning | Användaren autentiserades medan regeln för att alla ska kunna ändras vid autentisering var på plats för det valda PDF-dokumentet. | Alternativt kan du informera användaren om att han/hon får kostnadsfri tillgång till tjänsten på grund av MVPD-svårigheter. | n/a | Ja | Ja | Ja från 3.2 |
| N011 | Info | Användaren autentiserades med TempPass. | - Informera användaren. <br> <br> - Du kan också visa en lista över vanliga MVPD. | Du kan även logga in med ditt vanliga MVPD-program. | Ja | Ja | Ja från 3.2 |
| N111 | Varning | TempPass har gått ut. | - Informera användaren. <br> <br> - Presentera en lista över vanliga flerkanalsprogram. <br> <br> - Dölj alternativet TempPass. | Logga in med ditt vanliga MVPD. | Ja | Ja | Ja från 3.2 |
| N130 | Fel | **Autentiseringstoken hittades inte i sessionen.**  Detta kan bero på något av följande: <br> <br> 1. Webbläsaren har (från tredje part) cookies inaktiverade (gäller inte för AccessEnabler JavaScript SDK version 4.x) <br> <br> 2. Webbläsaren har alternativet Förhindra spårning över webbplatser aktiverat (Safari 11+) <br> <br> 3. Sessionen har upphört <br> <br> 4. Programmeraren anropar autentiserings-API:er i felaktig följd <br> <br> Obs! Den här felkoden är inte tillgänglig för omdirigeringsflöden på helsidan. | 1. Be användaren att aktivera cookies (från tredje part) <br> <br> 2. Be användaren att inaktivera spårning mellan webbplatser <br> <br> 3. Uppmana användaren att autentisera igen <br> <br> 4. Anropa API:er i rätt ordning | 1. Aktivera cookies (från tredje part) <br> <br> 2. Inaktivera spårning över flera webbplatser <br> <br> 3. Återautentisera <br> <br> 4. Ej tillämpligt | Ja | Ja | Ja från 3.2 |
| N500 | Fel | Internt fel. <br> <br> Obs! Det här är det ursprungliga felsystemets &quot;Generic Authentication Error&quot; och &quot;Internal Authentication Error&quot;. Det här felet kommer till slut att fasas ut. | Använd AccessEnablerDebug och inspektera felsökningsloggar (console.log output) för att avgöra vad som gick fel. | n/a | Ja | Ja | n/a |
| R401 | Fel | Det uppstod ett fel när en åtkomsttoken skulle hämtas. <br> <br> Obs! Detta är ett oåterkalleligt fel. Informera användaren om att programmet inte är tillgängligt. | - iOS: Kontrollera programsatsen och anpassade scheman i programmet. <br> <br> - JavaScript: Kontrollera programsatsen i webbprogrammet. <br> <br> Öppna en biljett med Zendesk och informera användaren om att systemet inte är tillgängligt för tillfället | n/a | Ja från v4.0 | Ja från v3.0 | Ja från 3.2 |
| R400 | Fel | Programmet är inte registrerat. Programsatsen är ogiltig eller har återkallats. <br> <br> Obs! Detta är ett oåterkalleligt fel. Informera användaren om att programmet inte är tillgängligt. | - iOS: Kontrollera programsatsen och anpassade scheman i programmet. <br> <br> - JavaScript: Kontrollera programsatsen i webbprogrammet. <br> <br> Öppna en biljett med Zendesk och informera användaren om att systemet inte är tillgängligt för tillfället | n/a | Ja från v4.0 | Ja från v3.0 | Ja från 3.2 |
| REG500 | Fel | Det gick inte att hämta registreringskoden från servern. <br> <br> Obs! Detta är ett oåterkalleligt fel. Informera användaren om att programmet inte är tillgängligt. | Öppna en biljett med Zendesk och informera användaren om att systemet inte är tillgängligt för tillfället. | n/a | Ja från v4.0 | Ja från v3.0 | Ja från 3.2 |
| REGCODE | Lyckades | Programmet anropade setSelectedProvider API på tvOS-plattformen. | Instruera/uppmana användaren att använda en andra enhet (skärm) för att logga in med den angivna registreringskoden. | Använd regcode på en andra enhet (skärm) för att initiera autentisering. | n/a | Ja endast för tvOS | n/a |
| Z010 | Varning | Användaren autentiserades medan nedbrytningsregeln authenticate-all eller authorized-all fanns på plats för det valda MVPD-programmet. | Alternativt kan du informera användaren om att han/hon får kostnadsfri tillgång till tjänsten på grund av MVPD-svårigheter. | n/a | Ja | Ja | Ja från 3.2 |
| Z011 | Info | Användaren auktoriserades med TempPass | Du kan även informera användaren | n/a | Ja | Ja | Ja från 3.2 |
| Z100 | Fel | Auktoriseringen misslyckades eftersom användaren inte har någon prenumeration för den begärda resursen eller på grund av andra orsaker som kommer från MVPD, t.ex. att videon inte matchar inställningarna för Föräldrakontroll för användarkontot | - Tillåt inte uppspelning. <br> <br> - Informera användaren. <br> <br> - The message key in the error message MAY contain a more detailed message provided by the MVPD. | n/a | Ja | Ja | Ja från 3.2 |
| Z110 | Fel | Behörighet nekades på grund av upprepade nekanden av MVPD. Möjligt försök till bedrägeri eller DOS. | - Tillåt inte uppspelning. <br> <br> - Informera användaren. | n/a | Ja | Ja | Ja från 3.2 |
| Z120 | Fel | Auktorisering nekas på grund av tekniska skäl vid kommunikation med det enhetliga dokumentationsdokumentet. Möjligt nätverksfel. | - Tillåt inte uppspelning. <br> <br> - Informera användaren om att MVPD hade problem och bör försöka senare. | Försök senare. | Ja | Ja | Ja från 3.2 |
| Z130 | Fel | Behörighet nekades eftersom en ogiltig/felformaterad resurs användes. | Kontrollera resurssträngen och korrigera den. I allmänhet beror det här felet antingen på en felaktig MRSS eller på att en oformaterad sträng används i stället för MRSS. | n/a | Ja | Ja | Ja från 3.2 |
| Z169 | Fel | Autentisering nekas eftersom authzNone-nedbrytningsregel har tillämpats för den angivna resursen. | Informera användaren | n/a | Ja | Ja | Ja från 3.2 |
| Z500 | Fel | Internt fel. <br> <br>  Obs! Detta är det gamla felet&quot;Allmänt autentiseringsfel&quot; och&quot;Internt autentiseringsfel&quot;. Det här felet kommer till slut att fasas ut. | Använd AccessEnablerDebug och inspektera felsökningsloggar (console.log output) för att avgöra vad som gick fel. | n/a | Ja | Ja | Ja från 3.2 |
| P100 | Fel | Förhandsauktoriseringen misslyckades. Det beror troligtvis på att du har begärt tillstånd för för många resurser. | - Använd INTE fler än det maximala antalet tillåtna resurser. <br> <br> - Kontakta Adobe Primetime autentiseringssupport för att hitta/ställa in maximalt antal tillåtna resurser. | n/a | Ja från v3.0 | Ja | Ja från 3.2 |
| IS2XX | Fel | Dessa felkoder returneras när personaliseringsserverns slutpunktssvarsdata har ett ogiltigt format eller saknar nödvändig individualiseringsinformation. | Öppna en biljett med Zendesk och informera användaren om att systemet inte är tillgängligt för tillfället | n/a | Ja från v3.0 | n/a | n/a |
| IS4XX | Fel | Dessa felkoder returneras vid fel på slutpunkten för individualiseringsservern 4XX - är HTTP-statuskoden för svaret. | Öppna en biljett med Zendesk och informera användaren om att systemet inte är tillgängligt för tillfället | n/a | Ja från v3.0 | n/a | n/a |
| IS5XX | Fel | Dessa felkoder returneras vid fel på slutpunkten för individualiseringsservern 5XX - är HTTP-statuskoden för svaret. | Öppna en biljett med Zendesk och informera användaren om att systemet inte är tillgängligt för tillfället | n/a | Ja från v3.0 | n/a | n/a |
| IS0 | Fel | Koden returneras när slutpunkten för individualiseringsservern inte svarar alls, därför har anslutningen uppnått en tidsgräns | Öppna en biljett med Zendesk och informera användaren om att systemet inte är tillgängligt för tillfället | n/a | Ja från v3.0 | n/a | n/a |
| LS011 | Varning | AccessEnabler använder ett instabilt lagringsutrymme på grund av LSO-/LocalStorage-problem och WebStorage-problem (eller otillgänglighet). <br> <br> Autentisering/auktorisering finns inte längre än den aktuella sidan! Varje sidinläsning gör att användaren måste autentisera. Konfigurerade TTL:er används inte vid sidomladdning. | - Informera användaren om begränsningar. <br> <br> - Informera användaren om hur man ökar det tillgängliga lagringsutrymmet. <br> <br> - Du kan även logga ut för att rensa lagringsutrymmet. | - Öka lagringsutrymmet. <br> <br> - Logga ut för att rensa lagringsutrymmet. | Ja | n/a | n/a |

<br>

## Ursprunglig felrapportering {#original-error-reporting}

I det här avsnittet beskrivs det ursprungliga felrapporteringssystemet tillsammans med de ursprungliga felkoderna. I det ursprungliga felrapporteringssystemet skickar AccessEnabler fel till dessa två callback-funktioner: `setAuthenticationStatus()` efter ett samtal till `checkAuthentication()`; `tokenRequestFailed()`, efter att ett anrop till `checkAuthorization()` eller `getAuthorization()`.

Den ursprungliga felrapporteringen och status-API:n fortsätter att fungera exakt som tidigare. Om du fortsätter uppdateras emellertid inte de ursprungliga felrapporterings-API:erna. Alla nya felrapporter och uppdateringar av gamla fel visas ENDAST i den nya [Avancerat felrapporteringssystem](#advanced-error-reporting).


Exempel på hur du använder det ursprungliga felrapporteringssystemet finns i [JavaScript API-referens](/help/authentication/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) och [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) funktioner, [API-referens för iOS/tvOS](/help/authentication/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)och [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed), [Android API-referens](/help/authentication/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) och [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### Ursprungliga felkoder för återanrop {#original-callback-error-codes}

| **Allmänna fel** | |
|---|---|
| Internt fel | Ett systemfel uppstod vid försök att bearbeta begäran. |
| Fel: Providern är inte vald | Inträffar när kunden avbryter i dialogrutan för val av leverantör. |
| Providern är inte tillgänglig | Inträffar när inga providers är tillgängliga. |
|  |  |
| **Autentiseringsfel** | |
| Allmänt autentiseringsfel | Returneras när orsaken inte är känd eller inte kan publiceras. |
| Internt autentiseringsfel | Ett systemfel uppstod vid försök att autentisera. |
| Användaren är inte autentiserad | Användaren är inte autentiserad. |
|  |  |
| **Auktoriseringsfel** |  |
| Allmänt auktoriseringsfel | Returneras när orsaken inte är känd eller inte kan publiceras. |
| Internt auktoriseringsfel | Ett systemfel uppstod vid försök att auktorisera. |
| Användaren är inte auktoriserad | Kunden har inte behörighet att visa det begärda innehållet. |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->
