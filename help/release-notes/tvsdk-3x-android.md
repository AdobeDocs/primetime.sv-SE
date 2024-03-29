---
title: Versionsinformation om TVSDK 3.15 för Android
description: Versionsinformation för TVSDK 3.15 för Android beskriver vad som är nytt eller ändrat, de lösta och kända problemen samt enhetsproblemen i TVSDK Android 3.15
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5516'
ht-degree: 0%

---

# Versionsinformation om TVSDK 3.15 för Android {#tvsdk-for-android-release-notes}

Versionsinformationen för TVSDK 3.15 för Android beskriver vad som är nytt eller ändrat, de lösta och kända problemen samt enhetsproblemen i TVSDK Android 3.15.

Android-referensspelaren ingår i Android TVSDK i katalogen samples/ i din distribution. I den medföljande README.md-filen beskrivs hur du skapar referensspelaren.

>[!NOTE]
>
>Om du vill skapa referensspelaren, enligt beskrivningen i README.md som distribueras med versionen, måste du göra följande:
>
>1. Hämta VideoHeartbeat.jar från [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (VideoHeartbeat-bibliotek för Android v2.0.0)
>1. Extrahera VideoHeartbeat.jar till mappen libs/.

TVSDK för Android har många prestandaförbättringar jämfört med tidigare versioner. Den ger en tittarupplevelse av hög kvalitet och innehåller alla funktioner i version 1.4, med undantag för Multi-CDN-stöd.

Den omfattande uppsättningen funktioner som stöds och inte stöds finns i [Funktionsmatris](#feature-matrix) i versionsinformationen.

## Android TVSDK 3.15

Den här versionen åtgärdar ett problem där programmet kraschar flera gånger när en kreativ tagg saknas eller när [!UICONTROL url CDATA] är tom i [!UICONTROL VAST] svar.

Mer information om felkorrigeringarna i den här och tidigare versioner finns i [problem som har korrigerats i TVSDK för Android](#resolved-issueszd).

### Nya funktioner och förbättringar i tidigare versioner

**Android TVSDK 3.14**

Den här versionen åtgärdar ett problem där programmet kraschar när [!UICONTROL CDATA] noden är tom för någon av [!UICONTROL ClickTracking], [!UICONTROL CustomClick] eller [!UICONTROL CompanionClickTracking] element i VAST-svar.

**Android TVSDK 3.13**

DRM-strömmar av vitt skilda slag fryser eller visar svarta bildrutor på ABR-omkopplare på FireTV-enheter, som innehåller 3:e generationens Fire TV-enheter av typen Pendant och Fire TV Cube 1:a och 2:a generationen.

Lös problemet genom att ange API:t `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` för de angivna Fire TV-enheterna innan uppspelningen startar. Standardvärdet är false.

**Android TVSDK 3.12**

Primetime Reference Application’s gradle version updated to version 5.6.4.

Följ instruktionerna från Viktigt-filen som finns i TVSDK-zippen på `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

De vanligaste problemen som åtgärdas i den aktuella versionen beskrivs i [lösta problem](#resolved-issues) -avsnitt.

**Android TVSDK 3.11**

* **PSSH-boxhämtning tillåts** - TVSDK tillåter hämtning av den systemspecifika rubrikruta för skydd som är associerad med den aktuella inlästa medieresursen. Nytt API `getPSSH()` läggs till i `com.adobe.mediacore.drm.DRMManager`.

Mer information finns i [DRM, Widewin](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

Versionen fokuserade på att åtgärda de vanligaste kundproblemen som nämns i [lösta problem](#resolved-issues) -avsnitt.

**Android TVSDK 3.9**

* **Säker leverans över HTTPS** - Android TVSDK 3.9 introducerade säkra leveransfunktioner via HTTPS för att leverera innehåll säkert i oöverträffad skala och prestanda.

  För säker leverans via HTTPS introducerades ett nytt API i `NetworkConfiguration` klassen.

  `public void setForceHTTPS (boolean value)`

  `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **Stöd för pre-roll med partiell annonsbrytning** - Med den här förbättringen stöder TVSDK 3.8 pre-roll ads med partiell Ad-Break-funktion (PABI).

Förhandsgranskningsannonsen spelas upp, om en sådan finns, och sedan spelas innehållet upp från den direktpunkt som emulerar upplevelsen av live-TV.

**Android TVSDK 3.7**

* För testinnehåll av typen Widewin: ett nytt API `setMediaDrmCallback` i klassen DRMManager exponeras för att åsidosätta standardimplementeringen av MediaDrmCallback-gränssnittet.

  `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* Åtgärdat AppCrash-fel för att inte hantera `MediaPlayerEvent.ITEM_UPDATED` i C++-lager (Android 64 bitar).

**Android TVSDK 3.6**

* **Förbättra dina appar för 64-bitarskrav** - det inbyggda biblioteket `(libAVEAndroid.so)` är nu uppgraderat och tillgängligt i två versioner. Den befintliga 32-bitarsbiblioteksplatsen för armeabi har ändrats från `/framework/Player to /framework/Player/armeabi` och ytterligare ett arm64-v8a-bibliotek (64 bitar) introduceras i `/framework/Player/arm64-v8a.`

**Version 3.5**

* **Just in Time Ad Resolution** - TVSDK 3.5 tar bort stödet för de annonser som spelas upp från tidslinjen.

* **Aktiverat stöd för uppspelning offline** - Med offlineuppspelning kan användare nu hämta videoinnehåll till sina enheter och titta på det när de inte är anslutna. Mer information finns i[Uppspelning offline med Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf).&quot;

**Version 3.4**

* TVSDK har nu stöd för CMAF-direktuppspelning för CBC-krypterade och rena strömmar.

**Version 3.3**

* **API-ändringar**

   * Ett nytt API läggs till i `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` för att hantera nätverksfel och timeout.
      * där (n) är antalet återförsök.

**Version 3.2**

* **Stöd för parallell annonsupplösning och hämtning av manifest**

   * TVSDK 3.2 stöder den samtidiga upplösningen i stället för den sekventiella upplösningen för alla annonsbegäranden och annonsbrytningar utom för VMAP.

   * Alla annonsmanifestationer i en annonsbrytning hämtas samtidigt.

* **Aktiverat stöd för tidsgräns för annonsupplösning och hämtning av manifest.**

   * Användarna kan nu ange timeout-värdet för den övergripande annonsupplösningen och för hämtning av manifest.  För VMAP gäller timeoutvärdet för enskilda annonsbrytningar när alla annonsbrytningar åtgärdas sekventiellt.

* **Introducerade nya API:er i klassen AdvertisingMetadata:**

   * `void setAdResolutionTimeout(int adResolutionTimeout)`

   * `int getAdResolutionTimeout()`

   * `void setAdManifestTimeout(int adManifestTimeout)`

   * `int getAdManifestTimeout()`

* **Borttagen nedan API:er från klassen AdvertisingMetadata:**

   * `void setAdRequestTimeout(int adRequestTimeout)`

   * `int getAdRequestTimeout()`

* **Aktiverad uppspelning av strömmar med AC3/EAC3-ljudkodek**

   * `void alwaysUseAC3OnSupportedDevices(boolean val)` in `MediaPlayer` class

* **TVSDK har stöd för CMAF och uppspelning av oformaterade strömmar för krypterad Wideglobal CTR.**

* **Uppspelning av HEVC-strömmar med 4K stöds nu.**

* **Parallella och anropsbegäranden** - TVSDK förhämtar nu 20 begäranden om annonsanrop parallellt.

**Version 3.0**

* **TVSDK 3.0 stöder HEVC-strömmar (High Efficiency Video Coding).**

* **Just in Time - Lösa annonser närmare annonsmarkörer**
Lazy Ad Resolving löser nu alla annonsbrytningar oberoende av varandra. Tidigare var annonsupplösningen en tvåstegsmetod: pre-rolls löstes innan uppspelningen startades och alla &quot;middle/post roll&quot;-kortplatser kombinerades efter att uppspelningen startades. Med den här förbättrade funktionen löses nu alla annonsbrytningar vid en viss tidpunkt före annonsreferenspunkten.

>[!NOTE]
>
>Lazy Ad Resolving har nu inaktiverats som standard och måste aktiveras explicit.

Ett nytt API läggs till i `AdvertisingMetadata::setDelayAdLoadingTolerance` för att få den fördröjda annonsinläsningstoleransen som är kopplad till dessa Advertising-metadata.\
Sökningar är nu tillåtna direkt efter PREPARATION, och sökning efter över annonsbrytningar ger en omedelbar lösning innan sökningen är klar.\
Signeringslägen `SERVER_MAP` och `MANIFEST_CUES` stöds.

Mer information finns i [TVSDK 3.0 for Android Programmer&#39;s Guide](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) på API- och händelseändringar.

* **Uppdaterat `targetSdkVersion` till den senaste versionen**

Uppdaterat `targetSdkVersion` från 19 till 27 för smidig funktion.

* **Placement.Type getPlacementType() är nu en metod i gränssnittet TimelineMarker**

  Den här metoden returnerar placeringstypen Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL eller Placement.Type.POST_ROLL. Om en annonsbrytning inte löses returnerar metoden getDuration() i gränssnittet TimelineMarker 0.

**Version 2.5.6**

* **TVSDK 2.5 har stöd för Android P.**

* **Aktivera bakgrundsljud**

  Om du vill aktivera ljuduppspelning när appen flyttas från förgrunden till bakgrunden ska appen anropa `enableAudioPlaybackInBackground` API för MediaPlayer med värdet true som argument när spelaren är i tillståndet PREPARED.

* **alwaysUseAudioOutputLatency(booleskt val) i klassen MediaPlayer**

Använd fördröjning för utdata vid beräkning av ljudtidsstämpling.
Booleska parametrar val - True använder fördröjning för ljudutgång vid beräkning av ljudtidsstämpling.

* **Optimerad för att få bästa möjliga uppspelningsupplevelse även om bandbredden plötsligt faller av**

TVSDK avbryter nu hämtning av det pågående segmentet om det behövs och växlar dynamiskt till lämplig återgivning. Detta görs genom att du sömlöst växlar mellan bithastigheterna utan avbrott.

**Version 2.5.5**

* **Inläggning av delvis annonsbrytning**

  TV-liknande upplevelse av att gå med mitt i en annons utan att aktivera spårningen för den delvis bevakade annonsen.\
  Exempel: Användaren går med i mitten (vid 40 sekunder) av en 90-sekunders annonsbrytning som består av tre 30-sekunders annonser. Detta är tio sekunder in i den andra annansen i pausen.

   * Den andra annonsen spelas upp för den återstående längden (20 sek) följt av den tredje annonsen.

   * Ad trackers for the part ad ad ad ad (second ad) are not fire. Spåraren för endast den tredje annonsen aktiveras.

* **Säker annonsinläsning över HTTPS**

  Adobe Primetime har ett alternativ för att begära att få ett första anrop till en primetime-annonsserver och CRS via https.

* **AdSystem och Creative ID har lagts till i CRS-begäranden**

  Nu med `AdSystem` och `CreativeId` som nya parametrar i förfrågningarna 1401 och 1403.

* **API setEncodeUrlForTracking i klassen NetworkConfiguration har tagits bort** eftersom osäkra tecken i en URL-adress ska kodas.

**Version 2.5.4**

Android TVSDK v2.5.4 erbjuder följande uppdateringar och API-ändringar:

* Ändringar i standardvärdet för `WebViewDebbuging`

  `WebViewDebbuging` värdet är inställt på `Fals`som standard. Om du vill aktivera det ringer du `setWebContentsDebuggingEnabled(true)` i programmet.

* **Uppgradering av OpenSSL- och Curl-version**

  Uppdaterat libcurl till v7.57.0 och OpenSSL till v1.0.2k.

* Åtkomst på appnivå för VAST-svarsobjekt

  Introducerade ett nytt API `NetworkAdInfo::getVastXml()` som ger åtkomst till VAST-svarsobjektet till programmet.

**Version 2.5.3**

Android TVSDK v2.5.3 erbjuder följande uppdateringar och API-ändringar.

* Alla TVSDK-kunder som använder CRS uppmanas att uppgradera sina appar med TVSDK 2.5.3.85 eller senaste på Android. Detta kommer att ersätta den befintliga programimplementeringen. Efter TVSDK-uppgraderingen söker du efter CRS Creative URL-begäranden i ett proxyverktyg (t.ex. Charles) och bekräftar att värdnamnet och versionen i sökvägen återspeglas som i exempelstrukturen nedan.

  `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK:s användaragent kan anpassas: vi har lagt till några nya API:er för att anpassa användaragenterna.

   * `setCustomUserAgent(String value)`
   * `getCustomUserAgent()`

* Dela cookies mellan Android-program och TVSDK: Android TVSDK har nu stöd för åtkomst av cookies mellan JAVA-lager (lagras i CookieStore i Android-programmet) och C++ TVSDK-lagret. Nu går det att ange och/eller ändra cookies i ursprungligt C++-lager eftersom de kommer att exponeras för Java Cookie Store.

* API-ändringar:

   * En ny händelse `CookiesUpdatedEvent` läggs till. Den skickas av mediaspelaren när dess cookie uppdateras.

   * Ett nytt API läggs till i `NetworkConfiguration::set/ getCustomUserAgent()` om du vill använda en anpassad användaragent.

   * Ett nytt API läggs till i `NetworkConfiguration::set/ getEncodedUrlForTracking` för att tvinga fram kodning av osäkra tecken.

   * Ett nytt API läggs till i `NetworkConfiguration::getNetworkDownVerificationUrl()` för att ange en URL för nätverksverifiering om en redundans uppstår.

   * En ny egenskap läggs till i `TextFormat::treatSpaceAsAlphaNum` som anger om mellanrum ska behandlas som alfanumeriskt när bildtexter visas.

* Ändringar i `SizeAvailableEvent`. Tidigare `getHeight()` och `getWidth()` metoder `SizeAvailableEvent` i 2.5.2 används för att returnera bildrutehöjd och bildrutebredd, som returnerades av medieformatet. Nu returneras den utdatahöjd respektive utdatavärde som returneras av avkodaren.

* Förändringar i Buffering-beteende: Buffring-beteende ändras. Det överlåts åt apputvecklaren om vad de vill göra om bufferten är tom. 2.5.3 använder uppspelningsbuffertstorlek vid tom buffertsituation.

**Version 2.5.2**

Android TVSDK v2.5.2 innehåller viktiga felkorrigeringar och några API-ändringar.

**Version 2.5.1**

De viktiga nya funktionerna i Android 2.5.1.

* **Prestandaförbättringar -** Den nya TVSDK 2.5.1-arkitekturen ger ett antal prestandaförbättringar. Baserat på statistik från en jämförande studie från tredje part ger den nya arkitekturen en 5 gånger kortare starttid och 3,8 gånger färre uteslutna bildrutor jämfört med branschens genomsnitt:

* **Direkt aktiverad för VOD och live -** När du aktiverar direkt, initierar och buffrar TVSDK media innan uppspelningen startar. Eftersom du kan starta flera MediaPlayerItemLoader-instanser samtidigt i bakgrunden kan du buffra flera strömmar. När en användare ändrar kanalen och strömmen har buffrats korrekt startar uppspelningen på den nya kanalen omedelbart. TVSDK 2.5.1 har även stöd för Instant On för **live** strömmar också. De aktiva strömmarna buffras om när det aktiva fönstret flyttas.

* **Förbättrad ABR-logik -** Den nya ABR-logiken baseras på buffertlängd, förändringshastighet för buffertlängd och uppmätt bandbredd. Detta garanterar att ABR väljer rätt bithastighet när bandbredden ändras och även optimerar antalet gånger som bithastighetsväxlingen faktiskt sker genom att övervaka den hastighet med vilken buffertlängden ändras.

* **Nedladdning av delar av segment/delsegmentering -** TVSDK minskar ytterligare storleken på varje fragment så att uppspelningen kan börja så snart som möjligt. Dess fragment måste ha en nyckelbildruta varannan sekund.

* **Lazy ad resolution -** TVSDK väntar inte på att icke-förhandsvisade annonser ska matchas innan uppspelningen startar, vilket minskar starttiden. API:er som sökning och uppspelning är fortfarande inte tillåtna förrän alla annonser är lösta. Detta gäller för VOD-strömmar som används med CSAI. Åtgärder som att söka och snabbt framåt är inte tillåtna förrän annonsupplösningen är slutförd. För liveströmmar kan den här funktionen inte aktiveras för annonsupplösning under en live-händelse.

* **Beständiga nätverksanslutningar -** Med den här funktionen kan TVSDK skapa och lagra en intern lista över beständiga nätverksanslutningar. De här anslutningarna återanvänds för flera begäranden i stället för att en ny anslutning öppnas för varje nätverksbegäran och sedan tas bort. Detta ökar effektiviteten och minskar fördröjningen i nätverkskoden, vilket ger snabbare uppspelningsprestanda.
När TVSDK öppnar en anslutning uppmanas servern att ange en *keep-alive* anslutning. Vissa servrar kanske inte stöder den här typen av anslutning. I så fall kommer TVSDK att återgå till att skapa en anslutning för varje begäran igen. Även om beständiga anslutningar är aktiverade som standard har TVSDK nu ett konfigurationsalternativ så att program kan inaktivera beständiga anslutningar om så önskas.

* **Parallell hämtning -** Att hämta video och ljud parallellt i stället för i serie minskar startfördröjningarna. Den här funktionen gör att HLS Live- och VOD-filer kan spelas upp, optimerar den tillgängliga bandbreddsanvändningen från en server, minskar sannolikheten att hamna i buffertunderkörningssituationer och minimerar fördröjningen mellan hämtning och uppspelning.

* **Parallella annonshämtningar -** TVSDK förhämtar annonser parallellt med innehållsuppspelningen innan annonsuppspelningen avbryts, vilket möjliggör smidig uppspelning av annonser och innehåll.

* **Uppspelning**

* **Uppspelning av MP4-innehåll -** Korta MP4-klipp behöver inte omkodas för att spelas upp i TVSDK.

  >[!NOTE]
  >
  >ABR-växling, tricks play, annonsinfogning, sen ljudbindning och undersegmentering stöds inte för MP4-uppspelning.

* **Trick play med adaptiv bithastighet (ABR) -** Med den här funktionen kan TVSDK växla mellan iFrame-strömmar i trickuppspelningsläge. Du kan använda profiler som inte är iFrame-profiler för att trigga uppspelningen med lägre hastigheter.

* **Smidigare tricks -** De här förbättringarna förbättrar användarupplevelsen:

   * Anpassad bithastighet och bildrutefrekvensval under uppspelning, baserat på bandbredd och buffertprofil

   * Använd huvudströmmen i stället för IDR-strömmen för att få upp till 30 fps snabb uppspelning.

* **Skydd av innehåll**

   * **Upplösningsbaserat utdataskydd -** Den här funktionen kopplar uppspelningsbegränsningar till specifika upplösningar och ger mer detaljerade DRM-kontroller.

* **Stöd för arbetsflöden**

   * **Direkt faktureringsintegrering -** Detta skickar faktureringsmätningar till Adobe Analytics, som certifieras av Adobe Primetime för strömmar som används av kunden.

  TVSDK samlar automatiskt in mätvärden och följer kundförsäljningskontraktet för att generera periodiska användningsrapporter som krävs för faktureringsändamål. I varje direktuppspelningshändelse använder TVSDK Adobe Analytics API för att skicka faktureringsvärden som innehållstyp, aktiverade markeringar för annonsinfogning och DRM-aktiverade flaggor - baserat på den fakturerbara strömmens varaktighet - till den rapportserie som ägs av Adobe Analytics Primetime. Detta stör inte och ingår inte i kundens egna Adobe Analytics-rapporteringsprogram eller serversamtal. På begäran skickas den här rapporten över faktureringsanvändning regelbundet till kunderna. Detta är den första fasen av faktureringsfunktionen som endast stöder fakturering av användning. Den kan konfigureras baserat på försäljningskontraktet med hjälp av de API:er som beskrivs i dokumentationen. Den här funktionen är aktiverad som standard. Se exemplet på referensspelaren om du vill inaktivera den här funktionen.

   * **Förbättrat stöd för failover -** Ytterligare strategier har implementerats för att fortsätta oavbruten uppspelning, trots fel på värdservrar, spellistfiler och segment.

* **Reklam**

   * **Moat Integration -** Stöd för visning av annonser från Moat.

   * **Companion banners -** Banderoller visas tillsammans med en linjär annons och fortsätter ofta att visas i vyn när annonsen är slut. Dessa banners kan vara av typen html (ett HTML-kodfragment) eller iframe (en URL till en iframe-sida).

* **Analyser**

   * **VHL 2.0 -** Det här är den senaste optimerade VHL-integreringen (Video Heartbeats Library) för automatisk insamling av användningsdata för Adobe Analytics. API:ernas komplexitet har minskat för att underlätta implementeringen. Hämta VHL-biblioteket [v2.0.0 för Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) och extrahera JAR-filen i mappen libs.

* **SizeAvaliableEventListener**

   * `getHeight()` och `getWidth()` metoder `SizeAvailableEvent` kommer nu att returnera utdata i höjd och bredd. Visningsproportioner kan beräknas på följande sätt:

     ```java
     SizeAvailableEvent e;
     DAR = e.getWidth()/ e.getHeight();
     ```

     Du kan också använda lagringsproportioner i form av bredd och höjd på stapel för att beräkna ramens bredd och höjd:

     ```java
     SAR = e.getSarWidth()/e.getSarHeight();
     frameHeight = e.getHeight();
     frameWidth = e.getWidth()/SAR;
     ```

* **Cookies**

   * Android TVSDK har nu stöd för åtkomst till JAVA-cookies som lagras i CookieStore i Android-programmet. Ett återanrops-API (onCookiesUpdated) tillhandahålls för att spela in när en ny cookie kommer som en del av **Set-Cookie** Svarshuvud. Dessa cookies är tillgängliga som en lista över HttpCookie(s) som används för en annan URI/domän genom att ange dessa cookie-värden på den aktuella URI/domänen med CookieStore. På samma sätt uppdateras cookie-värdena i TVSDK med API:t för CookieStore-tillägg.

## Funktionsmatris {#feature-matrix}

TVSDK för Android har stöd för ett antal funktioner som du kan implementera för att lägga till funktioner i dina videoprogram.

I funktionstabellerna nedan anger &quot;Y&quot; att funktionen stöds i den aktuella versionen.

| Funktion | Innehållstyp | HLS |
|---|---|---|
| Allmän uppspelning (Play, Pause, Seek) | VOD + Live | Y |
| FER - Allmän uppspelning (Play, Pause, Seek) | FER VOD | Y |
| Sök när en annons spelas upp | VOD + Live | Stöds inte |
| HEVC-uppspelning | VOD + Live | Endast fMP4-behållare |
| AC3 och EAC3 | VOD + Live | Stöds inte |
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
| Inläggning av delvis annonsbrytning | Live | Y |

| Funktion | Innehållstyp | HLS |
|---|---|---|
| AES-kryptering | VOD + Live | Y |
| AES-kryptering - exempel | VOD + Live | Y |
| Tokeniserade strömmar | VOD + Live | Y |
| DRM, Widewin | VOD + Live | Endast fMP4-behållare |
| Primetime DRM | VOD + Live | Y |
| Extern uppspelning (RBOP) | VOD + Live | Endast Primetime DRM |
| Licensrotation | VOD + Live | Endast Primetime DRM |
| Nyckelrotation | VOD + Live | Endast Primetime DRM |

| Funktion | Innehållstyp | HLS |
|---|---|---|
| Integrering med Adobe Analytics VHL | VOD + Live | Y |
| Fakturering | VOD + Live | Y |

## Lösta problem {#resolved-issues}

Där upplösning är kopplad till ett rapporterat problem visas en Zendesk-referens, till exempel ZD#xxxxx.

**Android TVSDK 3.15**

I det här avsnittet finns en sammanfattning av problemet som löstes i TVSDK 3.14 Android-versionen.

* ZD#46903 - Programmet kraschar flera gånger när en kreativ tagg saknas eller när [!UICONTROL url CDATA] är tom i [!UICONTROL VAST] svar.

**Android TVSDK 3.14**

* ZD#46903 - Programmet kraschar när [!UICONTROL CDATA] noden är tom för någon av [!UICONTROL ClickTracking], [!UICONTROL CustomClick] eller [!UICONTROL CompanionClickTracking] element i [!UICONTROL VAST] svar.

### Lösta problem i tidigare versioner

**Android TVSDK 3.12**

* ZD#40584 - Primetime Reference-appen byggs inte med den senaste övertoningsversionen.

**Android TVSDK 3.11**

* ZD#41252 - Koreanska tecken i WebVTT fungerar inte efter Android 7.1.

**Android TVSDK 3.10**

* ZD#40340 - Programmet kraschar med felet&quot;App Not Responding&quot; vid uppspelningsförsök efter blocklistning av alla TS-filer (TypeScript).

**Android TVSDK 3.8**

* Inga nya utgåvor har lagts till.

**Android TVSDK 3.7**

* Inga nya utgåvor har lagts till.

**Android TVSDK 3.6**

* Inga nya utgåvor har lagts till.

**Version 3.5**

* ZD#37503 - JSON-svar för CRS-regler cachelagras för att undvika dubblettbegäranden.

**Version 3.4**

* ZD#37996 - Korrigerade ett problem med uppspelning av hackning för Linjär och VOD CMAF HEVC-strömmar.
* ZD#37706 - Korrigerade ett problem med förvrängda bildtexter.
* ZD#37622 - Korrigerade ett problem med allvarliga URISyntaxErrors för specifika annonser.
* ZD#36938 - Korrigerade ett problem med att växla bithastighet ned till den mittersta bithastigheten och sedan hämta upp till den högsta bithastigheten efter att utskriften ur tricket har spelats upp.

**Version 3.3**

* ZD#37394 - Snabbt CMAF-objekt orsakar artefakter efter att hastigheten har ändrats.
   * Korrigerade ett problem som uppstod med en profiländring under uppspelning.
* ZD#37396 - Ad tracking-händelser saknas för vissa mellanrullningar och efterrullningar.
   * Korrigerade ett specifikt fall runt annonsuppföljningshändelser.
* ZD#37491 - HTTP-statuskod med felmetadata saknas.
   * Arbetade med att sprida nätverksfel högre upp i stacken.
* ZD#37808 - Tillåtelselista Ny anpassad rubrik.
   * Stöd för SSAI_TAG har lagts till som en del av den här korrigeringen.
* ZD#37622 - URISyntaxfel från specifika AD Pods.
   * Korrigerat ett problem med krasch vid direktuppspelning när kundens Android-app hanteras annonser som innehåller en okodad %
* ZD#37631 - Mastermanifeståterförsöksmekanism för Android TVSDK.
   * Nytt API har lagts till i nätverkskonfigurationen för hantering av den här förbättringen. Om API:t inte används görs inget nytt försök att skapa manifestet. Om det används kommer manifestet att provas igen för att hantera nätverksfel och timeout.

**Version 3.2**

* ZD#37493- Spårningsfyrar för live-uppspelning aktiveras inte regelbundet för den första annonsen i sekvensen.
* ZD#36985- Spårningsfyrar skickas inte för tomma annonsbrytningar i VMAP-svar.
* ZD#37134 - TVSDK returnerar fel ID för VMAP-svar ibland.

**Version 3.0**

* ZD#33740 - TVSDK genererar en varning som inte behövs precis efter att ett MediaPlayer-objekt har skapats och replaceCurrentResource() anropas

   * Förbättrade den tidigare korrigeringen genom att anropa restore endast när spelaren är i pausat läge

* ZD#36442 - Varje ny uppspelning kopplar från fjärrfelsökningssession, vilket gör det omöjligt att felsöka.

   * Felsökning är inte möjligt som standard i webbvyn eftersom felsökning inte är aktiverat som standard. Programmet bör aktivera felsökning om det behövs genom att anropa setWebContentsDebuggingEnabled(true) för objekt som returneras från MediaPlayer.getCustomAdView().

* ZD#33688 - Stöd för Just In Time och upplösning

   * Annonsbrytningar löses vid ett angivet intervall före positionen för annonsbrytningen.

* ZD#36441 - Livefönstrets varaktighet fortsätter att öka i mer än 5 minuter och orsakar flera problem.

   * Korrigerade ett problem där virtualStartTime lades till två gånger vid beräkning av virtuell direktpunkt, vilket resulterade i det här problemet.

**Android TVSDK 2.5.6**

* ZD #34992 - Språket är tomt i undertextrutan.

   * Korrigerade ett fall där TVSDK inte parsade #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS från huvudmanifestet för att få information om bildtextspår.

* ZD #35078 - Android P-validering.

   * TVSDK 2.5.6 har validerats med de senaste betaversionerna av Android P. Inga problem hittades på grund av det nya Android OS.

* ZD #34149 - Spelaren fortsätter att begära manifest även om ett fel påträffas.

   * Korrigerade fallet där TVSDK gjorde upprepade anrop även när alla profiler var nere (fel 404).

* ZD #31533 - Spela upp ljud på Android när programmet har skickats till bakgrunden.

   * Tillagd `enableAudioPlaybackInBackground` API för MediaPlayer som ska anropas med &quot;True&quot; som argument (när spelaren är i läget PREPARED) för att aktivera uppspelning av ljud när appen är i bakgrunden.

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK meddelar 640x368 när den faktiska videostorleken är 640x360.

   * På grund av att variabeln m_nOutputHeight (i AndroidMCVideoDecoder) uppdateras med bildrutehöjd i stället för den faktiska utdatahöjden. Genomför relevanta ändringar i funktionen getVideoFrame för att beräkna m_nOutputHeight korrekt.

* ZD #26614 - Urgent - 3rd party ad annonsservning/programmatic - failed to service imponsions.

   * Förbättrade den tidigare korrigeringen genom att hantera fallet i XML-tolkning där problemet kunde reproduceras när&quot;space&quot; är före&quot;equal&quot;-tecknet som &lt;vast version=&quot;2.0&quot;>

* ZD #29296 - Android: Lägg till AdSystem och Creative ID i CRS-begäranden.

   * Inkludera nu AdSystem och CreativeId som nya parametrar i förfrågningarna 1401 och 1403.

* ZD #33062 - TVSDK kraschar vid förekomst av lodstreck i VAST-svar under CDATA-nod

   * API setEncodeUrlForTracking i klassen NetworkConfiguration har tagits bort som osäkra tecken i en URL som ska kodas

* ZD #33063 - Logiken för val av CRS-fil avbröts - TVSDK skickade inte CRS-begäran för webbformat utan skickade den i stället för 3gpp-filer.

   * Laga logiken nu. När du använder mediefiler med webm- och 3gpp-format skickas en CRS-begäran för webben. Och om du använder båda mediefilerna i 3gpp-format skickas CRS-begäran för den högsta bithastigheten i 3gpp-filen.

* ZD #33125 - Android-appen kraschar med en specifik DoubleClick-tagg i VMAP.

   * Scenariot har åtgärdats för att undvika kraschen.

* ZD #32256 - Problem med licensrotation och nyckelrotation - Adobe Access

   * Korrigerade initieringen av segment med DRM-metadata för SampleAES-innehåll. Fungerar bra med AES128-innehåll.

* ZD #33619 - Snabbspolning av ett växande spellistinnehåll som fastnat i buffringsläge nära direktpunkten.

   * Hanteras när man korsar en direktpunkt i trickläge

* ZD #34151 - TimedMetadata-objekt är i fel ordning.

   * Två TimedMetadata-händelser visades i slumpmässig ordning om de tillhörde samma tid på tidslinjen. De bibehöll sin ursprungliga order i manifestet.

* ZD #34189 - Problem vid försök till början av annonsbrytning.

   * Problemet var SSAI-annonser som sammanfogats med kontinuitet. Och orsaken var ett beteende när vi sökte till början av sådana annonser, vi sökte efter en nyckelbildruta och vi hittade den inte. Orsaken var att annonsens lägsta tidsstämpel för ljud var före min tidsstämpel för video. Därför söker vi efter en nyckelbildruta vid fel fragmentDump-data. Åtgärdat nu.

* ZD #34528 - Videoupplösning som inte uppgraderas utöver 640x360 på 3:e generationens FireTV-dongel.

   * Förbättrad korrigering för att inkludera de senaste uppdateringarna av inbyggd programvara

* ZD #34793 - TVSDK 2.5.x brukade krascha med anpassad innehållsupplösare i vissa fall när VideoEngine antog att audioSettings var tillgängliga och inte var det.

   * Kraschen inträffade på grund av ett funktionsanrop på en delad Null-pekare (audiudeSettings). En villkorlig kontroll har lagts till i VideoEngineTimeline::placeToSourceTimeline() för att kontrollera att audiudeSettings är tillgängligt innan du anropar något i det objektet.

* ZD #32584 - Det går inte att komma åt fullständig information i &lt;extensions> nod för ett VAST-svar.

   * Problemet med XML-tolkning har åtgärdats och NetworkAdInfo innehåller nu den fullständiga informationen i &lt;extensions> nod

* ZD #35086 - Hämtar inte fullständiga tilläggsdata från spelaren om det finns specifika VMAP-svar.

   * Problemet var specifikt för XML-tillägg eftersom XML-tolkning inte fungerade om XML-tillägget hade dubbla citattecken inom attributvärdet. Åtgärdade problemet.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Uppspelningssession som aktiverar fjärrfelsökning för webbvyn.

WebViewDebbuging är som standard inställt på False. Om du vill aktivera felsökning anger du som true via programmet med setWebContentsDebuggingEnabled(true).

* ZenDesk#33011 - Annonstidslinjen löses inte om en CRS-begäran misslyckas.

  När en CRS-begäran till en annons misslyckas, löses tidslinjen och de återstående annonserna spelas upp.

* ZenDesk#34528 - Videoupplösningen uppgraderar inte längre än 640x360 på tredje generationens FireTV-dongel.

  Videoupplösningen växlar uppåt när bithastigheten ändras.

* ZenDesk#33192 - AudioTrack har null-namn när spåret hämtas via AudioUpdatedEventListener::onAudioUpdated.

  I ett fåtal scenarier på FireTV Stick utlöstes onAudioUpdate-händelsen när det inte fanns någon faktisk ljuduppdatering. Det här är nu löst.

**Android TVSDK 2.5.3**

* Zendesk#32216 - Prenumerationen på den anpassade taggen TimedMetadata fungerar inte.

  Vi returnerar ID3-data som en bytearray (som har stöd för APIC eller generiska data) till klienten medan 1.4 returnerar en sträng. Byte-arrayen hanterar inte själva tecknet som avslutas med null, och därför visades ett specialtecken för klienten. Problemet har åtgärdats nu.
* Zendesk#32670 - Spelaren misslyckas inte över till spellistan Redundant

  Detta fungerar nu som det ska och setNetworkDownVerificationUrl fungerar som förväntat.
* Zendesk#32369 - Dold bildtext visar olika typer av färgplagg eller artefakter.

  Problem med CC-fel har korrigerats i den senaste versionen
* Zendesk#25590 - Förbättra: TVSDK cookie store ( C++ till JAVA )

  Android TVSDK har nu stöd för åtkomst av cookies mellan JAVA-lager (som lagras i CookieStore i Android-programmet) och C++ TVSDK-lagret.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 verkar inte ha korrigeringen för PTPLAY-20269

  Problemet har åtgärdats och integrerats i 2.5.2-grenen.
* Zendesk#31806 - Auditude-käppar i BEREDNING

  Spelaren fastnade i tillståndet Förbereder eftersom XML för svar hade en tom tagg. Problemet är nu åtgärdat.
* Zendesk#31727 - TVSDK 2.5 med undertexter tas bort eller felstavas.

  Problemet är åtgärdat och vi släpper/felstavar inga tecken.
* Zendesk#31485 - DrmManager in 2.5

  Ett problem uppstod när DRMManager skapades via nya DrmManager (kontextkontext). En implementerad DRMService-klass som skulle ge DRMManager.
* Upplösningsströmmen Zendesk#32794-1080P spelas inte upp på Android

  Vi har ändrat metoderna SizeAvailableEvent och Tidigare, getHeight() och getWidth() för SizeAvailableEvent i 2.5 som används för att returnera bildrutehöjd och bildrutebredd, som returnerades av medieformatet. Den returnerar nu utdatahöjd och utdatavärde som returneras av avkodaren.
* Flashen Player Zendesk #19359 kraschar på grund av positionen för #EXT-X-FAXS-CM-attributet i manifestet på uppsättningsnivå.

  Taggen #EXT-X-FAXS-CM måste alltid finnas i den övre spellistan innan enskilda bithastigheter eller segment visas i spellistan.

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

  I VMAP XML om det finns en tom VAST-tagg utan en explicit avslutande tagg (&quot;&lt;/vast>&#39;) och utan ett radmatningstecken efter det tolkas inte VMAP-XML korrekt och annonserna kanske inte kan spelas upp.

**Android TVSDK 2.5.1**

* Enhetsspecifik (Samsung Galaxy Tab 4) krasch; VOD DRM LBA med Auditude och klicka på annonserna.
* VHL - Felaktiga hjärtslagsanrop skickas när innehåll från en förskjutning startas.
* När VPAID-annonser spelas upp anropas händelsen för VHL-pulsslag:type:play-annons saknas.
* När du har försatts i COMPLETE-status återgår spelaren till uppspelningsstatus med SKIP och BreakPolicy för postrollannonser.
* Cookies kopplas inte till utgående annonsåteranrop.
* Referenspunkter för annonser visas inte.
* HLS med separat EAC3 SAP-spår läses inte in.
* Spelaren kraschar när TVSDK får en Screen On-återgivning efter att Media Player har återställts.

## Kända fel och begränsningar {#known-issues-and-limitations}

**Android TVSDK 3.11**

* Inga nya begränsningar har lagts till.

### Kända fel och begränsningar i tidigare versioner

**Android TVSDK 3.10**

* Inga nya begränsningar har lagts till.

**Android TVSDK 3.8**

* Inga nya begränsningar har lagts till.

**Android TVSDK 3.7**

* Inga nya begränsningar har lagts till.

**Android TVSDK 3.6**

* Inga nya begränsningar har lagts till.

**Android TVSDK 3.5**

* Ingen ny begränsning har lagts till.

**Android TVSDK 3.4**

* ID3, Closed Captions och Late Binding Audio har inte verifierats för CMAF-strömmen (CBC).
* På vissa enheter finns det ett problem med låg reproducerbarhet på grund av vilket videoförvrängning kan visas högst upp under trick play i CMAF-strömmar.

**Android TVSDK 3.3**

* clcp:c608-bildtexter stöds inte för CMAF-direktuppspelning.

**Android TVSDK 3.2**

* TVSDK 3.2 stöder inte uppspelning av strömmar med CMAF Sample AES och AES128.
* HEVC CMAF-strömmar har inte stöd för uppspelning av undertexter.
* Grön färgläggning visas för WV-krypterade strömmar när sökning utförs runt det okrypterade segmentet.
* CMAF-strömmar stöder inte ID3-händelser.
* HLS-strömmar stöder inte TTML-bildtextformat.

**Android TVSDK 3.0**

* HEVC-stödet har följande begränsningar i den här versionen

   * DRM stöds inte
   * Stöd för CC (CEA 608/708) har inte verifierats
   * 4K-stöd finns ännu inte
   * Stöd för ID3-taggar har inte verifierats

* För annonsförloppshändelser kanske tidslinjens fält inte visar 100 % korrekt annonsuppspelningstid. Som en tillfällig lösning kan man använda `adcompleteevent` för att ta reda på hur annonsuppspelningen slutförs och uppdatera användargränssnittet för olika syften, som att uppdatera tidslinjefältet, ta bort och relaterat användargränssnitt osv.
* Olika annonsanrop som returneras från VMAP följer inte lookahead-positionen just-in-time.

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
* I VMAP XML, om det finns en tom VAST-tagg utan en explicit avslutande tagg (&lt;/vast>), och utan en ny rad efter den, tolkas inte VMAP XML korrekt och annonserna kanske inte spelas upp.
* VPAID-post-roll stöds inte.

## Användbara resurser {#helpful-resources}

* [Systemkrav](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)
* [TVSDK 3.10 for Android Programmer&#39;s Guide](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-prod-audience-guide.md)
* [TVSDK Android Javadoc for API Reference](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [TVSDK Android C++ API-dokument](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) - Varje Java-klass har en motsvarande C++-klass, och C++-dokumentationen innehåller mer förklarande material än JavaOS, så se C++-dokumentationen för en mer detaljerad förståelse av Java API.
* [TVSDK 1.4 till 2.5 för migreringshandbok för Android (Java)](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* Information om hur du hanterar skärmbilder på/av finns i `Application_Changes_for_Screen_On_Off.pdf` som ingår i bygget.
* Se den fullständiga hjälpdokumentationen på [Adobe Primetime Läs mer &amp; Support](https://helpx.adobe.com/support/primetime.html) sida.
