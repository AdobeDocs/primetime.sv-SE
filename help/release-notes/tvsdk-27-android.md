---
title: Versionsinformation om TVSDK 2.7 för Android
description: Versionsinformationen för TVSDK 2.7 för Android beskriver vad som är nytt eller ändrat, de lösta och kända problemen samt enhetsproblemen i TVSDK Android 2.7
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '4095'
ht-degree: 0%

---


# Versionsinformation om TVSDK 2.7 för Android {#tvsdk-for-android-release-notes}

Versionsinformationen för TVSDK 2.7 för Android beskriver vad som är nytt eller ändrat, de lösta och kända problemen samt enhetsproblemen i TVSDK Android 2.7

## TVSDK Android 2.7 {#tvsdk-android}

Android-referensspelaren ingår i Android TVSDK i katalogen samples/ i din distribution. I den medföljande README&lt;.md-filen beskrivs hur du skapar referensspelaren.

>[!NOTE]
>
>Om du vill skapa referensspelaren, enligt beskrivningen i README.md som distribueras med versionen, måste du göra följande:
>
>1. Hämta VideoHeartbeat.jar från [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (VideoHeartbeat-bibliotek för Android v2.0.0)
>1. Extrahera VideoHeartbeat.jar till mappen libs/.

>



## Nya funktioner {#new-features}

TVSDK 2.7 för Android innehåller alla funktioner i version 1.4 förutom de funktioner som inte stöds i [Funktionsmatris](#feature-matrix).

**Android TVSDK 2.7**

* **Stöd för parallell annonsupplösning**

TVSDK 2.7 stöder den samtidiga upplösningen av alla Ad-begäranden i en Ad break i stället för sekventiell upplösning.

### Nya funktioner i tidigare versioner {#new-features-previous-releases}

**Version 2.5.6**

* **TVSDK 2.5 har stöd för Android P**
* **Aktivera bakgrundsljud**

   Om du vill aktivera ljuduppspelning när appen flyttas från förgrunden till bakgrunden ska appen anropa enableAudioPlaybackInBackground API för MediaPlayer med värdet true som argument när spelaren är i tillståndet PREPARED.

* **alwaysUseAudioOutputLatency(booleskt val) i klassen MediaPlayer**

Använd fördröjning för utdata vid beräkning av ljudtidsstämpling.
Booleska parametrar val - True använder fördröjning för ljudutgång vid beräkning av ljudtidsstämpling.

* **Optimerad för att få bästa möjliga uppspelningsupplevelse även om bandbredden plötsligt faller av.**
TVSDK avbryter nu hämtning av det pågående segmentet om det behövs och växlar dynamiskt till lämplig återgivning. Detta görs genom att du sömlöst växlar mellan bithastigheterna utan avbrott.

**Version 2.5.5**

* **Inläggning av delvis annonsbrytning**

   TV-liknande upplevelse av att gå med mitt i en annons utan att aktivera spårningen för den delvis bevakade annonsen.\
   Exempel**: **Användaren går med i mitten (vid 40 sekunder) av en 90-sekunders annonsbrytning som består av tre 30-sekunders annonser. Detta är tio sekunder in i den andra annansen i pausen.
   * Den andra annonsen spelas upp för den återstående längden (20 sek) följt av den tredje annonsen.
   * Ad trackers for the part ad ad ad ad (second ad) are not fire. Spåraren för endast den tredje annonsen aktiveras.

* **Säker annonsinläsning över HTTPS**

   Adobe Primetime har ett alternativ för att begära att primetime-annonsservern och CRS ska ringa via https.

* **AdSystem och Creative ID har lagts till i CRS-begäranden**

   * Inkludera nu AdSystem och CreativeId som nya parametrar i förfrågningarna 1401 och 1403.

* **API setEncodeUrlForTracking i klassen NetworkConfiguration** tas bort eftersom osäkra tecken i en URL ska kodas.

**Version 2.5.4**

Android TVSDK v2.5.4 erbjuder följande uppdateringar och API-ändringar:

* Ändringar i standardvärdet för WebViewDebuging
Värdet för WebViewDebbuging är som standard False. Om du vill aktivera det anropar du setWebContentsDebuggingEnabled(true) i programmet.
* Uppgradering av OpenSSL- och Curl-version
Uppdaterat libcurl till v7.57.0 och OpenSSL till v1.0.2 kB.
* Åtkomst på appnivå för VAST-svarsobjekt
Introducerade ett nytt API NetworkAdInfo::getVastXml() som ger åtkomst till VAST-svarsobjektet för programmet.

**Version 2.5.3**

Android TVSDK v2.5.3 erbjuder följande uppdateringar och API-ändringar.

* Alla TVSDK-kunder som använder CRS uppmanas att uppgradera sina appar med TVSDK 2.5.3.85 eller senaste på Android. Detta kommer att ersätta den befintliga programimplementeringen. Efter TVSDK-uppgraderingen söker du efter CRS Creative URL-begäranden i ett proxyverktyg (t.ex.: Charles) och bekräfta att värdnamnet och versionen i sökvägen återspeglas som i exempelstrukturen nedan.

   `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* Användaragent för TVSDK kan anpassas: har vi lagt till några nya API:er för att anpassa användaragenterna.

   * setCustomUserAgent(String-värde)
   * getCustomUserAgent()

* Dela cookies mellan Android-program och TVSDK: Android TVSDK har nu stöd för åtkomst av cookies mellan JAVA-lager (som lagras i CookieStore i Android-programmet) och C++ TVSDK-lagret. Nu går det att ange och/eller ändra cookies i ursprungligt C++-lager eftersom de kommer att exponeras för Java Cookie Store.
* API-ändringar:

   * En ny Event CookiesUpdatedEvent läggs till. Den skickas av mediaspelaren när dess cookie uppdateras.
   * Ett nytt API läggs till i NetworkConfiguration::set/ getCustomUserAgent() för att använda en anpassad användaragent.
   * Ett nytt API läggs till i NetworkConfiguration::set/ getEncodedUrlForTracking för att framtvinga kodning av osäkra tecken.
   * Ett nytt API läggs till i NetworkConfiguration::getNetworkDownVerificationUrl() för att ange en URL för nätverksverifiering om en redundans uppstår.
   * En ny egenskap läggs till i TextFormat::treatSpaceAsAlphaNum som definierar om mellanrum ska hanteras som alfanumeriskt när bildtexter visas.

* Ändringar i SizeAvailableEvent: Tidigare användes metoderna getHeight() och getWidth() för SizeAvailableEvent i 2.5.2 för att returnera bildrutehöjd och bildrutebredd, som returnerades av medieformatet. Nu returneras den utdatahöjd respektive utdatavärde som returneras av avkodaren.
* Förändringar i Buffering-beteende: Buffertbeteendet har ändrats. Det överlåts åt apputvecklaren om vad de vill göra om bufferten är tom. 2.5.3 använder uppspelningsbuffertstorlek vid tom buffertsituation.

**Version 2.5.2**

Android TVSDK v2.5.2 innehåller viktiga felkorrigeringar och några API-ändringar.

**Version 2.5.1**

De viktiga nya funktionerna i Android 2.5.1.

* **Prestandaförbättringar** Den nya TVSDK 2.5.1-arkitekturen ger ett antal prestandaförbättringar. Baserat på statistik från en jämförande studie från tredje part ger den nya arkitekturen en 5 gånger kortare starttid och 3,8 gånger färre uteslutna bildrutor jämfört med branschens genomsnitt:

   * **Direkt aktiverad för VOD och live -** När du aktiverar direkt initieras och buffrar TVSDK medier innan uppspelningen startar. Eftersom du kan starta flera MediaPlayerItemLoader-instanser samtidigt i bakgrunden kan du buffra flera strömmar. När en användare ändrar kanalen och strömmen har buffrats korrekt startar uppspelningen på den nya kanalen omedelbart. TVSDK 2.5.1 stöder även direktuppspelning på för **live**-strömmar. De aktiva strömmarna buffras om när det aktiva fönstret flyttas.

      * **Förbättrad ABR-logik -** Den nya ABR-logiken baseras på buffertlängd, hastighet för ändring av buffertlängd och uppmätt bandbredd. Detta garanterar att ABR väljer rätt bithastighet när bandbredden ändras och även optimerar antalet gånger som bithastighetsväxlingen faktiskt sker genom att övervaka den hastighet med vilken buffertlängden ändras.
      * **Delsegmentnedladdning/delsegmentering -** TVSDK minskar ytterligare storleken på varje fragment för att kunna starta uppspelningen så snart som möjligt. Dess fragment måste ha en nyckelbildruta varannan sekund.
      * **Lazy-annonsupplösning -** TVSDK väntar inte på upplösning av annonser som inte är preflight innan uppspelningen startar, vilket minskar starttiden. API:er som sökning och uppspelning är fortfarande inte tillåtna förrän alla annonser är lösta. Detta gäller VOD-strömmar som används med CSAI. Åtgärder som att söka och snabbt framåt är inte tillåtna förrän annonsupplösningen är slutförd. För liveströmmar kan den här funktionen inte aktiveras för annonsupplösning under en live-händelse.
      * **Beständiga nätverksanslutningar -** Med den här funktionen kan TVSDK skapa och lagra en intern lista över beständiga nätverksanslutningar. De här anslutningarna återanvänds för flera begäranden i stället för att en ny anslutning öppnas för varje nätverksbegäran och sedan tas bort. Detta ökar effektiviteten och minskar fördröjningen i nätverkskoden, vilket ger snabbare uppspelningsprestanda.
När TVSDK öppnar en anslutning uppmanas servern att ange en *keep-alive*-anslutning. Vissa servrar kanske inte stöder den här typen av anslutning. I så fall kommer TVSDK att återgå till att skapa en anslutning för varje begäran igen. Även om beständiga anslutningar är aktiverade som standard har TVSDK nu ett konfigurationsalternativ så att program kan inaktivera beständiga anslutningar om så önskas.
      * **Parallell nedladdning -** Att hämta video och ljud parallellt i stället för i serie minskar startfördröjningarna. Den här funktionen gör att HLS Live- och VOD-filer kan spelas upp, optimerar den tillgängliga bandbreddsanvändningen från en server, minskar sannolikheten att hamna i buffertunderkörningssituationer och minimerar fördröjningen mellan hämtning och uppspelning.
      * **Parallella annonshämtningar -** TVSDK förhämtar annonser parallellt med innehållsuppspelningen innan annonsuppspelningen avbryts, vilket möjliggör smidig uppspelning av annonser och innehåll.

* **Uppspelning**

   * **MP4 Content Playback -** MP4 short clips do not need to be retranscoded to play back within TVSDK.
Obs! ABR-växling, tricks play, annonsinfogning, sen ljudbindning och undersegmentering stöds inte för MP4-uppspelning.
   * **Trick play med adaptiv bithastighet (ABR) -** Den här funktionen gör att TVSDK kan växla mellan iFrame-strömmar i trickuppspelningsläge. Du kan använda profiler som inte är iFrame-profiler för att trigga uppspelningen med lägre hastigheter.
   * **Smidigare tricks -** De här förbättringarna förbättrar användarupplevelsen:

          * Anpassad bithastighet och bildrutefrekvensval under trick play, baserat på bandbredd och buffertprofil
          * Använd huvudströmmen i stället för IDR-strömmen för att få upp till 30 fps snabb uppspelning.
      
* **Skydd av innehåll**

   * **Upplösningsbaserat utdataskydd -** Den här funktionen kopplar uppspelningsbegränsningar till specifika upplösningar, vilket ger mer detaljerade DRM-kontroller.

* **Stöd för arbetsflöden**

   * **Integrering med direkt fakturering -** Detta skickar faktureringsmätningar till Adobe Analytics, som certifieras av Adobe Primetime för strömmar som används av kunden.
TVSDK samlar automatiskt in mätvärden och följer kundförsäljningskontraktet för att generera periodiska användningsrapporter som krävs för faktureringsändamål. I varje direktuppspelningshändelse använder TVSDK Adobe Analytics API för att skicka faktureringsmått som innehållstyp, aktiverade markeringar för annonsinfogning och DRM-aktiverade flaggor - baserat på den fakturerbara strömmens varaktighet - till den rapportserie som ägs av Adobe Analytics Primetime. Detta stör inte och ingår inte i kundens egna Adobe Analytics-rapporteringsprogram eller serversamtal. På begäran skickas den här användningsrapporten regelbundet till kunderna. Detta är den första fasen av faktureringsfunktionen som endast stöder fakturering av användning. Den kan konfigureras baserat på försäljningskontraktet med hjälp av de API:er som beskrivs i dokumentationen. Den här funktionen är aktiverad som standard. Se exemplet på referensspelaren om du vill inaktivera den här funktionen.
   * **Förbättrat stöd för växling vid fel -** Ytterligare strategier som implementeras för att fortsätta uppspelningen utan avbrott, trots fel i värdservrar, spellistfiler och segment.

* **Reklam**

   * **Moat Integration -** Stöd för visning av annonser från Moat.
   * **Medföljande banderoller -** Medföljande banderoller visas tillsammans med en linjär annons och fortsätter ofta visas i vyn när annonsen är slut. Dessa banners kan vara av typen html (ett HTML-kodfragment) eller iframe (en URL till en iframe-sida).

* **Analyser**

   * **VHL 2.0 -** Det här är den senaste optimerade VHL-integreringen (Video Heartbeats Library) för automatisk insamling av användningsdata för Adobe Analytics. API:ernas komplexitet har minskat för att underlätta implementeringen. Hämta VHL-biblioteket [v2.0.0 för Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) och extrahera JAR-filen i mappen libs.

* **SizeAvaliableEventListener**
   * Metoderna getHeight() och getWidth() för SizeAvailableEvent returnerar nu utdata i höjd och bredd. Visningsproportioner kan beräknas enligt följande:

      ```
      SizeAvailableEvent e;
      
      DAR = e.getWidth()/ e.getHeight();
      
      Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:
      
      SAR = e.getSarWidth()/e.getSarHeight();
      
      frameHeight = e.getHeight();
      
      frameWidth = e.getWidth()/SAR;    
      ```

* **Cookies**

   * Android TVSDK har nu stöd för åtkomst till JAVA-cookies som lagras i CookieStore i Android-programmet. Ett återanrops-API (onCookiesUpdated) tillhandahålls för att spela in varje gång en ny cookie kommer som en del av svarsrubriken&quot;Set-Cookie&quot;. Dessa cookies är tillgängliga som en lista över HttpCookie(s) som används för en annan URI/domän genom att ange dessa cookie-värden på den aktuella URI/domänen med CookieStore. På samma sätt uppdateras cookie-värdena i TVSDK med API:t för CookieStore-tillägg.

## Funktionsmatris {#feature-matrix}

TVSDK för Android har stöd för ett antal funktioner som du kan implementera för att lägga till funktioner i dina videoprogram.

I funktionstabellerna nedan anger &quot;Y&quot; att funktionen stöds i den aktuella versionen.

| Funktion | Innehållstyp | HLS |
|---|---|---|
| Allmän uppspelning (Play, Pause, Seek) | VOD + Live | Y |
| FER - Allmän uppspelning (Play, Pause, Seek) | FER VOD | Y |
| Sök när en annons spelas upp | VOD + Live | Stöds inte |
| AC3 | VOD + Live | Stöds inte |
| MP3 | VOD | Stöds inte |
| Uppspelning av MP4-innehåll | VOD | Y |
| Adaptiv logik för växling av bithastighet | VOD + Live | Y |
| Uppspelning endast av ljud | VOD + Live | Y |
| Stöd för flera CDN | VOD + Live | Stöds inte |
| Uppspelning av annonser med media som bara innehåller ljud | VOD + Live | Stöds inte |
| Undertexter - 608/708 | VOD + Live | Y |
| Undertexter - WebVTT | VOD + Live | Y |
| Manifestväxling vid fel | VOD + Live | Y |
| Avancerad redundans | VOD + Live | Y |
| QoS och spelarmeddelanden | VOD + Live | Y |
| Stöd för cookie-rubriker | VOD + Live | Y |
| Stöd för anpassade HTTP-rubriker | VOD + Live | Y (tillåt att lista krävs) |
| Ange parametrar för buffertkontroll | VOD + Live | Y |
| Ange adaptiva bithastighetskontroller | VOD + Live | Y |
| Egna manifesttaggar | VOD + Live | Y |
| Sena ljudbindning | VOD + Live | Y |
| 302 Omdirigering | VOD + Live | Y |
| Uppspelning med förskjutning | VOD + Live | Y |
| Uppspelning endast av ljud | VOD + Live | Y |
| Trick Play | VOD + Live | Y |
| Långsam rörelse i Trick Play | VOD + Live | Stöds inte |
| Smooth Trick Play (med ABR) | VOD + Live | Y |
| ID3-parsning | VOD + Live | Y |
| Utbrott av annonser | VOD + Live | Stöds inte |
| Direkt på | VOD + Live | Stöds inte |
| Stöd för brytpunkter | VOD + Live | Y |
| 302 Omdirigera taggighet | VOD + Live | Y |

| Funktion | Innehållstyp | HLS |
|---|---|---|
| Allmän uppspelning, annonser aktiverade | VOD + Live | Y |
| FER-innehåll med annonser aktiverade | VOD | Y |
| Standardbeteenden för annonser | VOD + Live | Y |
| VAST 2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| MP4-annonser | VOD + Live | Y (från CRS) |
| Trick Play med annonser aktiverade | VOD + Live | Y |
| Endast annons | VOD | Y |
| Målparametrar | VOD + Live | Y |
| Egna parametrar | VOD + Live | Y |
| Anpassade annonsbeteenden | VOD + Live | Y |
| Anpassade annonstaggar | Live | Y |
| Anpassade annonslösare | VOD + Live | Y |
| Anpassad annonslösning för frihjulshjul | VOD | Y |
| C3 | VOD + Live | Stöds inte |
| Lazy Ad Resolve | VOD | Y |
| Stöd för brytpunkter - SSAI | VOD + Live | Y |
| Companion Ads, Banner Ads och Clickable Ads | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y (JS) |
| Tidigt annonsutträde | Live | Y |
| Regelbaserad kreativ prioritering | VOD + Live | Y |
| CRS-regler | VOD + Live | Y |
| JSON Ad Resolver | VOD + Live | Stöds inte |
| Moat Integration | VOD + Live | Y |

| Funktion | Innehållstyp | HLS |
|---|---|---|
| AES-kryptering | VOD + Live | Y |
| AES-kryptering - exempel | VOD + Live | Y |
| Tokeniserade strömmar | VOD + Live | Y |
| DRM | VOD + Live | Primetime DRM only (Future: WideVM) |
| Extern uppspelning (RBOP) | VOD + Live | Endast Primetime DRM |
| Licensrotation | VOD + Live | Endast Primetime DRM |
| Nyckelrotation | VOD + Live | Endast Primetime DRM |

| Funktion | Innehållstyp | HLS |
|---|---|---|
| Integrering med Adobe Analytics VHL | VOD + Live | Y |
| Fakturering | VOD + Live | Y |

## Lösta problem {#resolved-issues}

Där upplösning är kopplad till ett rapporterat problem visas en Zendesk-referens, till exempel ZD#xxxxx

**Android TVSDK 2.7**

Detta avsnitt innehåller en sammanfattning av det problem som löstes i TVSDK 2.7-versionen.

* ZD#37166 - Anrop om felspårning utlöses även när annonsen spelas upp som den ska.
* ZD#37134 - Fel ID för annonsering returneras om wrapper(3P) Ad finns med flera annonser i VMAP-svaret.

**Android TVSDK 2.5.6**

* ZD #34992 - Språket är tomt i undertextrutan.
   * Korrigerade ett fall där TVSDK inte parsade #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS från huvudmanifestet för att få information om bildtextspår.
* ZD #35078 - Android P-validering.
   * TVSDK 2.5.6 har validerats med de senaste betaversionerna av Android P. Inga problem hittades på grund av det nya Android-operativsystemet.
* ZD #34149 - Spelaren fortsätter att begära manifest även om ett fel påträffas.
   * Korrigerade fallet där TVSDK gjorde upprepade anrop även när alla profiler var nere (fel 404).
* ZD #31533 - Spela upp ljud på Android när programmet har skickats till bakgrunden.
   * Lagt till `enableAudioPlaybackInBackground`-API för MediaPlayer som ska anropas med True som argument (när spelaren är i läget PREPARED) för att aktivera uppspelning av ljud när appen är i bakgrunden.

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK meddelar 640x368 när den faktiska videostorleken är 640x360.
   * På grund av att variabeln m_nOutputHeight (i AndroidMCVideoDecoder) uppdateras med bildrutehöjd i stället för den faktiska utdatahöjden. Genomför relevanta ändringar i funktionen getVideoFrame för att beräkna m_nOutputHeight korrekt.
* ZD #26614 - Urgent - 3rd party ad annonsservning/programmatic - failed to service imponsions.
   * Förbättrade den tidigare korrigeringen genom att hantera fallet i XML-tolkning där problemet kunde reproduceras när&quot;space&quot; är före&quot;equal&quot;-tecknet som &lt;VAST version =&quot;2.0&quot;>
* ZD #29296 - Android: Lägg till AdSystem och Creative ID i CRS-begäranden.
   * Inkludera nu AdSystem och CreativeId som nya parametrar i förfrågningarna 1401 och 1403.
* ZD #33062 - TVSDK kraschar vid förekomst av lodstreck i VAST-svar under CDATA-nod
   * API setEncodeUrlForTracking i klassen NetworkConfiguration har tagits bort som osäkra tecken i en URL som ska kodas.
* ZD #33063 - Logiken för val av CRS-fil avbröts - TVSDK skickade inte CRS-begäran för webbformat utan skickade den i stället för 3gpp-filer.
   * Laga logiken nu. När du använder mediefiler med webm- och 3gpp-format skickas en CRS-begäran för webben. Och om du använder båda mediefilerna i 3gpp-format skickas CRS-begäran för den högsta bithastigheten i 3gpp-filen.
* ZD #33125 - Android-appen kraschar med en specifik DoubleClick-tagg i VMAP.
   * Scenariot har åtgärdats för att undvika kraschen.
* ZD #32256 - Problem med licensrotation och nyckelrotation - Adobe Access.
   * Korrigerade initieringen av segment med DRM-metadata för SampleAES-innehåll. Fungerar bra med AES128-innehåll.
* ZD #33619 - Snabbspolning av ett växande spellistinnehåll som fastnat i buffringsläge nära direktpunkten.
   * Hanterades fallet när man korsade direktpunkten i trickläge.
* ZD #34151 - TimedMetadata-objekt är i fel ordning.
   * Två TimedMetadata-händelser visades i slumpmässig ordning om de tillhörde samma tid på tidslinjen. De bibehöll sin ursprungliga order i manifestet.
* ZD #34189 - Problem vid försök till början av annonsbrytning.
   * Problemet var SSAI-annonser som sammanfogats med kontinuitet. Och orsaken var ett beteende när vi sökte till början av sådana annonser, vi sökte efter en nyckelbildruta och vi hittade den inte. Orsaken var annonsens lägsta tidsstämpel för ljud före min tidsstämpel för video. Därför söker vi efter en nyckelbildruta vid fel fragmentDump-data. Åtgärdat nu.
* ZD #34528 - Videoupplösning som inte uppgraderas utöver 640x360 på 3:e generationens FireTV-dongel.
   * Förbättrad korrigering med de senaste uppdateringarna av inbyggd programvara.
* ZD #34793 - TVSDK 2.5.x brukade krascha med anpassad innehållsupplösare i vissa fall när VideoEngine antog att audioSettings var tillgängliga och inte var det.
   * Kraschen inträffade på grund av ett funktionsanrop på en delad Null-pekare (audiudeSettings). En villkorlig kontroll har lagts till i VideoEngineTimeline::placeToSourceTimeline() för att kontrollera att audiudeSettings är tillgängligt innan du anropar något i det objektet.
* ZD #32584 - Det går inte att komma åt fullständig information som finns i noden &lt;Extensions> för ett VAST-svar.
   * Problemet med XML-tolkning har åtgärdats och NetworkAdInfo tillhandahåller nu den fullständiga informationen i noden &lt;Extensions>.
* ZD #35086 - Hämtar inte fullständiga tilläggsdata från spelaren för specifika VMAP-svar.
   * Problemet var specifikt för XML-tillägg eftersom XML-tolkning inte fungerade om XML-tillägget hade dubbla citattecken inom attributvärdet. Åtgärdade problemet.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Uppspelningssession som aktiverar fjärrfelsökning för webbvyn.
   * WebViewDebbuging är som standard inställt på False. Om du vill aktivera felsökning anger du som true via programmet med setWebContentsDebuggingEnabled(true).
* ZenDesk#33011 - Annonstidslinjen löses inte om en CRS-begäran misslyckas.
   * När en CRS-begäran till en annons misslyckas, löses tidslinjen och de återstående annonserna spelas upp.
* ZenDesk#34528 - Videoupplösningen uppgraderar inte längre än 640x360 på tredje generationens FireTV-dongel.
   * Videoupplösningen växlar uppåt när bithastigheten ändras.
* ZenDesk#33192 - AudioTrack har null-namn när spåret hämtas via AudioUpdatedEventListener::onAudioUpdated.
   * I ett fåtal scenarier på FireTV Stick utlöstes onAudioUpdate-händelsen när det inte fanns någon faktisk ljuduppdatering. Det här är nu löst.

**Android TVSDK 2.5.3**

* Zendesk#32216 - Prenumerationen på den anpassade taggen TimedMetadata fungerar inte.
   * Vi returnerar ID3-data som en bytearray (som har stöd för APIC eller generiska data) till klienten medan 1.4 returnerar en sträng. Byte-arrayen hanterar inte själva tecknet som avslutas med null, och därför visades ett specialtecken för klienten. Problemet har åtgärdats nu.
* Zendesk#32670 - Spelaren misslyckas inte över till spellistan Redundant
   * Detta fungerar nu som det ska och setNetworkDownVerificationUrl fungerar som förväntat.
* Zendesk#32369 - Dold bildtext visar olika typer av färgplagg eller artefakter.
   * Problem med CC-fel har korrigerats i den senaste versionen
* Zendesk#25590 - Förbättra: TVSDK cookie store (C++ till JAVA)
   * Android TVSDK har nu stöd för åtkomst av cookies mellan JAVA-lager (som lagras i CookieStore i Android-programmet) och C++ TVSDK-lagret.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 verkar inte ha korrigeringen för PTPLAY-20269
Problemet har åtgärdats och integrerats i 2.5.2-grenen.
* Zendesk#31806 - Auditude Stcks in PREPARING
Spelaren fastnade i tillståndet Förbereder eftersom XML för svar hade en tom tagg. Problemet är nu åtgärdat.
* Zendesk#31727 - TVSDK 2.5 med undertexter tas bort eller felstavas.
   * Problemet är åtgärdat och vi släpper/felstavar inga tecken.
* Zendesk#31485 - DrmManager in 2.5
   * Ett problem uppstod när DRMManager skapades via nya DrmManager (kontextkontext). En implementerad DRMService-klass som skulle ge DRMManager.
* Upplösningsströmmen Zendesk#32794-1080P spelas inte upp på Android.
   * Vi har ändrat metoderna SizeAvailableEvent och Tidigare, getHeight() och getWidth() för SizeAvailableEvent i 2.5, som används för att returnera ramhöjd och rambredd, som returnerades av medieformatet. Den returnerar nu utdatahöjd och utdatavärde som returneras av avkodaren.
* Zendesk #19359 Flash Player kraschar på grund av positionen för #EXT-X-FAXS-CM-attributet i manifestet på uppsättningsnivå.
   * Taggen #EXT-X-FAXS-CM måste alltid finnas i den övre spellistan innan enskilda bithastigheter eller segment visas i spellistan.

**Android TVSDK 2.5.2**

* Zendesk#17305 Artefakter i undertexter med ogenomskinlig bakgrund.
egenskapen setTreatSpaceAsAlphaNum i TextFormat visas. Som standard är egenskapen False. Ange egenskapen som True i en klient för att lösa problemet med mörkt utrymme.

* Zendesk#25097 CC-skärmen har visuella artefakter med CC-inställningar.
egenskapen setTreatSpaceAsAlphaNum i TextFormat visas. Som standard är egenskapen False. Ange egenskapen som True i en klient för att lösa problemet med mörkt utrymme.

* Zendesk #31620 Användaragentsträngen som lämnar TVSDK-spelaren trunkeras.
Användaragentsträngen kommer inte längre att trunkeras efter 128 tecken.
Adobe Primetime-versionssträng läggs till i systemanvändaragenten.

* Zendesk #30809 Saknad SEEK_END-händelse förhindrar att appen övergår till uppspelningsläge.
* Zendesk #30415 Closed Captions &#39;Cyan&#39;-färg är nu en mörkare nyans av blått (turkos) jämfört med tidigare Primetimes TVSDK-versioner.

   Färgen ändras från DarkCyan till Cyan.

* Zendesk #30727 VOD-annonser hämtas/löses inte.

   Om det finns en tom VAST-tagg utan en explicit avslutande tagg (&quot;&lt;/VAST>&quot;) i VMAP XML och det inte finns något radmatningstecken efter det tolkas inte VMAP-XML korrekt och annonserna kanske inte spelas upp.

**Android TVSDK 2.5.1**

* Enhetsspecifik (Samsung Galaxy Tab 4) krasch. VOD DRM LBA med Auditude och klicka på annonser.
* VHL - Felaktiga hjärtslagsanrop skickas när innehåll från en förskjutning startas.
* När VPAID-annonser spelas upp, saknas anrop från VHL-pulsslag för händelse:type:play och.
* När du har försatts i COMPLETE-status återgår spelaren till uppspelningsstatus med SKIP och BreakPolicy för postrollannonser.
* Cookies kopplas inte till utgående annonsåteranrop.
* Referenspunkter för annonser visas inte.
* HLS med separat EAC3 SAP-spår läses inte in.
* Spelaren kraschar när TVSDK får en Screen On-återgivning när Media Player har återställts.

## Kända fel och begränsningar {#known-issues-and-limitations}

**Android TVSDK 2.7**

* TVSDK 2.7 stöder samtidiga upplösningar på upp till 5 Ads.
* När det gäller VMAP-svar sker annonsanrop i en enda annonsbrytning samtidigt, och annonseringsbrytningarna löses sekventiellt.
* I FER löses annonsanrop i varje affärsmöjlighet samtidigt.

### Kända fel och begränsningar i tidigare versioner{#known-issues-limitations-previous-releases}

**Android TVSDK 2.5.6**

* Flera VMAP-annonbrytningar samtidigt stöds inte.

**Android TVSDK 2.5.3**

Den här versionen har följande problem:

* Livevideouppspelning kan ha problem med synkronisering av ljud och video på enheter med låg kvalitet eller dåliga nätverksförhållanden.
* För FER-strömmar kan virtualTime och localTime skilja sig åt. FER med förskjutning fungerar inte heller.
* Uppspelningen kan fastna när innehållet i Late Binding Audio söks igenom.
* WebVTT-bildtexter kan ibland bli osynkroniserade för LIVE-innehåll.
* Ibland kan snabb uppspelning av få bildrutor ses när annonsuppspelningen är slut.
* Ibland inträffar 303-fel för tre radbrytningar, även om annonser spelas upp.

**Android TVSDK 2.5.2**

Den här versionen har följande problem:

* Den aktiva videouppspelningen kan ha problem med ljud-video-synkronisering på enklare enheter.
* Uppspelningen kan avbrytas vid olika tillfällen när du söker till slutet av VOD-mediet.
* För FER-strömmar kan virtualTime och localTime skilja sig åt. FER med förskjutning fungerar inte heller.

**Android TVSDK 2.5.1**

Den här versionen av TVSDK har följande problem:

* Livevideouppspelning kan ha problem med synkronisering av ljud och video på avancerade enheter.
* För FER-strömmar kan virtualTime och localTime skilja sig åt. FER med förskjutning fungerar inte heller.
* Om det finns en tom VAST-tagg utan en explicit avslutande tagg (&lt;/VAST>) i VMAP XML, och utan en ny rad efter den, tolkas inte VMAP-XML korrekt och annonserna kanske inte spelas upp.
* VPAID-post-roll stöds inte.

## Användbara resurser {#helpful-resources}

* [Systemkrav](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-requirements.html)
* [TVSDK 2.7 for Android Programmer&#39;s Guide](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-2-7-for-android/overview/c-psdk-android-2_7-overview-prod-audience-guide.html)
* [TVSDK Android Javadoc for API Reference](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html)
* [TVSDK Android C++ API-dokument](https://help.adobe.com/en_US/primetime/api/psdk/cpp/namespaces.html) - Varje Java-klass har en motsvarande C++-klass och C++-dokumentationen innehåller mer förklarande material än Javadocs, så se C++-dokumentationen för en djupare förståelse av Java API.
* [TVSDK 1.4 till 2.5 för migreringshandbok för Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Information om hur du hanterar skärmscenarier på/av finns i `Application_Changes_for_Screen_On_Off.pdf`-filen som ingår i bygget.
* Läs den fullständiga hjälpdokumentationen på [Adobe Primetime Learn &amp; Support](https://helpx.adobe.com/support/primetime.html)-sidan.