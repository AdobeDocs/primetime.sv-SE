---
title: Versionsinformation om TVSDK 3.12 för iOS
description: Versionsinformationen för TVSDK 3.12 för iOS beskriver vad som är nytt eller ändrat, de lösta och kända problemen samt enhetsproblemen i TVSDK iOS 3.12.
translation-type: tm+mt
source-git-commit: 51b3713e04fcb4adeaa7a8d1b700372b1dba7cf6
workflow-type: tm+mt
source-wordcount: '7665'
ht-degree: 0%

---


# Versionsinformation för TVSDK 3.12 för iOS {#tvsdk-for-ios-release-notes}

Versionsinformationen för TVSDK 3.12 för iOS beskriver vad som är nytt eller ändrat, de lösta och kända problemen samt enhetsproblemen i TVSDK iOS 3.12.

## System- och programvarukrav {#system-software-requirements}

Innan du laddar ned iOS 3.12 bör du kontrollera att maskinvaru-, operativsystem- och programversionerna uppfyller följande krav:

Operativsystem: iOS 8.0 eller senare.

## iOS TVSDK 3.12

Korrigerade ett problem där direktuppspelningen misslyckades efter 15 minuters uppspelning.

Information om korrigeringar i den aktuella versionen finns i [Kundproblem som har korrigerats](#resolved-issues) och om begränsningar finns i [avsnittet Kända fel och begränsningar](#known-issues-and-limitations).

### Nya funktioner och korrigeringar i tidigare versioner {#whats-new-previous}

**iOS TVSDK 3.11**

Åtgärdade kundproblem där `isFallbackOnInvalidCreativeEnabled` och metoden `customParams` gör att programmet kraschar.

**iOS TVSDK 3.10**

* Korrigerade ett problem där TVSDK-spelaren inte utlöste `PTMediaPlayerStatusError`-meddelanden när nätverket inte är tillgängligt.

**iOS TVSDK 3.9**

* Ett problem har korrigerats där VTT-undertexter inte kan spelas upp vilket medför att appen fryser.

* iOS TVSDK 3.9 innehöll det uppdaterade personaliseringscertifikatet.

**Programfix för iOS TVSDK 3.8.0.83**

Snabbfixen hade det uppdaterade transportcertifikatet för personalisering.

**iOS TVSDK 3.8**

iOS 13-kompatibilitet och hanterad borttagning av API:t iOS 13 UIWebView.

**iOS TVSDK 3.7**

Programfix för ett scenario där uppspelningen stoppades när ett stort antal annonsförfrågningar gjordes samtidigt.

**iOS TVSDK 3.6**

**Korrigeringar i klassen av egenskapen wideXML`PTNetworkAdInfo`**

FantastiskXML-egenskap angavs inte korrekt och returnerade ett nollvärde.

**iOS TVSDK 3.5**

**Aktivera bakgrundsljud**

*Konfigurera appen så att ljudet fortsätter att spelas upp när den placeras i bakgrunden.*

För att aktivera den här funktionen måste vi ange det nya API:t `audioPlaybackInBackground` som lagts till i klassen PTMediaPlayer. När det här API:t är aktiverat kan ditt program spela upp bakgrundsljud.

**iOS TVSDK 3.4.0.19 (programfix)**

Den här versionen innehåller en korrigering för programkrascher som inträffar i ett ad failover-scenario.

**iOS TVSDK 3.4**

**Timeout för annonsupplösning**

* Med TVSDK 3.4 kan man nu ange timeoutvärdet för den övergripande annonsupplösningen och för nedladdningar av manifest. Om vissa annonser inte är tillgängliga inom en viss tidsgräns    löste sig kommer TVSDK att spela de återstående annonserna.

* PTAdMetadata: API:t adRequestTimeout har tagits bort och kommer att tas bort. Standardvärdet är 35 sekunder.

* Två nya alternativa API:er har introducerats i PTAdMetadataClass: adResolutionTimeout - timeout för allmänna annonsupplösningsanrop                adManifestTimeout - timeout för hämtningar av annonsmanifest.

**Intäktsoptimering**

Aktiverade TVSDK för att identifiera problemområden som rör arbetsflöden för annonsinfogning och rapportera till analysens slutpunkt.

**Version 3.3**

TVSDK 3.3 är nu kompatibelt med iOS 11 SDK. Alla föråldrade API:er har ersatts med lämpliga alternativ.

**Version 3.2**

**Stöd för ytterligare loggning (fas 2)**

Stöd för felmeddelanden har lagts till om:

* HLS-versionen av annonsen använder högre nivå än innehåll.

* Variant som endast är för ljud är exkluderad.

* VAST/VMAP-begäran misslyckades.

**Version 3.1**

* **Ytterligare**
loggningsstödStöd för beskrivande meddelanden vid fel vid annonsuppspelning.

* **Stöd**
för Fairplay-krypterad CMAF-strömStöd för Fairplay-krypterade CMAF-strömmar med AVC-kodekuppspelning stöds nu.

**Version 3.0.1**

Inga nya funktioner eller förbättringar i den här versionen.

**Version 3.0**

* TVSDK 3.0 stöder HEVC-strömmar.

* Just In Time - Matcha annonser närmare annonsmarkörer.

En `enableDelayAdLoading`-egenskap av Boolean-typ har lagts till i gränssnittet på appnivå för att aktivera JIT. Om `enableDelayAdLoading` är NO kommer det att `setadMetadata.delayAdLoading`vara True (egenskapen i PTAdMetadata-gränssnittet).

När den här egenskapen är aktiverad löser TVSDK alla annonsbrytningar före positionen baserat på det toleransvärde som har definierats. Som standard är `delayAdTolerance` inställt på 5 sekunder.

**Version 1.4.45**

För att uppfylla kraven i Xcode10 har TVSDK flyttat från `libstdc++` till `libc++`, och därför är den version som stöds som lägst iOS 7. Tidigare var det iOS 6.

**Version 1.4.44**

Inga nya funktioner eller förbättringar i den här versionen.

**Version 1.4.43**

* TV-liknande upplevelse av att kunna vara med mitt i en annons utan att aktivera spårning av delar av annonser.\
   Exempel: Användaren går med i mitten (vid 40 sekunder) av en 90-sekunders annonsbrytning som består av tre 30-sekunders annonser. Detta är tio sekunder in i den andra annansen i pausen.

   * Den andra annonsen spelas upp för den återstående längden (20 sek) följt av den tredje annonsen.
   * Annonsspårare för delvis uppspelade annonser (andra annonsen) aktiveras inte. Spåraren för endast den tredje annonsen aktiveras.

* Egenskapen enableVodPreroll av Boolean-typ har lagts till i PTAdMetadata-gränssnittet. Egenskapen kan användas för att aktivera förrullning i en VoD-ström. Om enableVodPreroll är NO spelas PSDK inte upp före rullning. Detta påverkar dock inte fabrikerna. Standardvärdet för enableVodPreroll är JA.
* closedCaptionDisplayEnabled API i PTMediaPlayer-gränssnittet har markerats som borttaget från och med iOS v1.4.43. Om du vill ta reda på om undertexter är tillgängliga för ett visst PTMediaPlayerItem ska du undersöka egenskapen subtitlesOptions för PTMediaPlayerMediaItem.

**Version 1.4.42**

Inga nya funktioner har lagts till i den här versionen. En lista över åtgärdade problem finns i [Lösta problem](#resolved-issues).

**Version 1.4.41**

API-ändringar:

* **isSecure**: Ett nytt API har introducerats: Skydda spelaren från att spela in och utlösa ett fel. Standardvärdet är true.

* **allowExternalRecording**: Ett nytt API har introducerats för att tillåta spegling av airplay för ett säkert innehåll. Airplay-spegling behandlas som inspelning och därför måste `allowExternalRecording`-värdet anges till `True`, för att tillåta airplay-spegling eller inställt på `False` för att stoppa airplay-speglingen för säkert innehåll. Som standard är `value` true.

**Version 1.4.40**

Inga nya funktioner.

**Version 1.4.39**

* iOS TVSDK är certifierat med VHL 2.0.1 och med VHL 2.0.1 med Nielsen.

* iOS TVSDK uppdateras för att göra CRS-begäranden från den nya Akamai-värden `primetime-a.akamaihd.net`.

* Den nya värdnamnskonfigurationen ger leverans av CRS-resurser via både HTTP och HTTPS (SSL) i större skala.

**Version 1.4.36**

Integrera och certifiera VHL 2.0 i iOS TVSDK: Minska barriären i implementeringen av `VideoHeartbeatsLibrary` genom att minska komplexiteten i API:erna.

**Version 1.4.34**

**Nätverksannonsinformation**

TVSDK API:er ger nu ytterligare information om VAST-svar från tredje part. Ad ID, Ad System och VAST Ad Extensions finns i klassen `PTNetworkAdInfo` som är tillgänglig via egenskapen `networkAdInfo` för en annonsresurs. Den här informationen kan användas för integrering med andra annonseringsplattformar som **Moat Analytics**.

**Version 1.4.31**

* **FaktureringsstatistikFör att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.** 

   Varje gång TVSDK genererar en direktuppspelningshändelse börjar spelaren att skicka HTTP-meddelanden regelbundet till Adobe faktureringssystem. Perioden, som kallas fakturerbar varaktighet, kan vara en annan för VOD av standardtyp, VOD av proffskvalitet (aktiverad annonsering i mellanrullar) och direktinnehåll. Standardlängden för varje innehållstyp är 30 minuter, men ditt kontrakt med Adobe avgör de faktiska värdena.

* **Multi-CDN-stöd för CRS** AdsTVSDK har nu stöd för Multi-CDN för CRS-annonser. Genom att ange FTP-information för CRS-annonser kan du ange CDN-platser, andra än det Adobe-ägda standardnätverket för CDN, till exempel Akamai.

**Version 1.4.29**

I klassen `PTSDKConfig` har API:t forceHTTPS lagts till.

Klassen `PTSDKConfig` innehåller metoder för att framtvinga SSL på begäranden som görs till Adobe Primetime annonsbesluts-, DRM- och Video Analytics-servrar. Mer information finns i metoderna `forceHTTPS` och `isForcingHTTPS` för den här klassen. Om ett manifest läses in via HTTPS, bevarar TVSDK innehållsanvändningen för HTTPS och respekterar denna användning när relativa URL:er läses in från det manifestet.

>[!NOTE]
>
>Begäranden till tredjepartsdomäner som annonsspårning av pixlar, innehålls- och annonsadresser och liknande förfrågningar ändras inte, och det är innehållsleverantörernas och annonsservrarnas ansvar att tillhandahålla URL:er som stöds via HTTPS.

**Version 1.4.18**

Primetime iOS TVSDK har nu stöd för VPAID 2.0 Javascript-kreatörer för en interaktiv annonsupplevelse i strömmen. Mer information om VPAID 2.0 finns i Stöd för VPAID-annonser.

**Version 1.4.17**

* tvOS

   TVSDK stöder inbyggda tvOS-program.
* Följande typer av innehåll kan spelas upp:

   * VOD
   * Live
   * AES-128
   * Alternativt ljud och undertexter
   * FER

* Följande typer av annonser kan visas:

   * Grundläggande
   * VAST2
   * VAST3
   * VMA

* Följande funktioner stöds för närvarande inte:

   * Digital Rights Management (DRM)
   * Annonsbanners
   * TV Markup Language (TVML)

**Version 1.4.13**

>[!NOTE]
>
>Nielsen-modulen har tagits bort från TVSDK-bygget och TVSDK kommer inom kort att uppdateras med en ny Nielsen-integreringsmodul.

**Ad Fallback, Daisy chaining in ad ad selection logic (Zendesk #3103)**

För VAST-annonser (kreatörer) med återgångsregeln aktiverad hanterar TVSDK en annons med en ogiltig MIME-typ som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet. Mer information finns i Lägga till reserv för VAST- och VMAP-annonser.

**Version 1.4.9**

**Svart signalering med alternativ innehållsersättning**

Som en del av uppdateringen 1.4 TVSDK stöder vi nu också att man går in i och tillbaka från regionala strömavbrott mot linjärt innehåll. TVSDK kan nu bearbeta två manifestfiler parallellt, i huvudversion och alternativt, för att övervaka utpressningssignaler även när alternativ programmering visas i stället för den ursprungliga programmeringen.

**Version 1.4.8**

**Video Heartbeats Library (VHL) uppdaterad till version 1.5**

* Möjlighet att skicka metadata med videostart och/eller video-/annons/kapitelstart som kontextdata.

* Mindre nätverkstrafik - antalet pulsslag är i genomsnitt mindre och mindre.

**Version 1.4.7**

* **Individuellt stöd**

Stöd för lokala installationer av Adobe Individualization Server för att anpassa klientens individualiseringsbegäran och gå till en annan slutpunkt.

* **Upplösningsbaserat utdataskydd**

DRM-profiler kan nu ange den högsta tillåtna upplösningen, beroende på enhetens utdataskyddsfunktioner. Exempel:&quot;Om HDCP är tillgängligt kan du tillåta att innehåll med en upplösning på upp till 1080p spelas upp, och om HDCP inte är tillgängligt kan du tillåta att innehåll med en upplösning på upp till 480p spelas upp.&quot;

**Version 1.4.4**

* **Video Heartbeats Library (VHL) update to version 1.4.1.1**

   * Lagt till möjlighet att paketera olika analysanvändningsfall, från andra SDK:er eller spelare, med Adobe Analytics Video Essentials.
   * Annonsspårning har optimerats genom att metoderna `trackAdBreakStart` och `trackAdBreakComplete` har tagits bort. Annonsbrytningen härleds från metodanropen `trackAdStart` och `trackAdComplete`.
   * Egenskapen `playhead` behövs inte längre när annonser spåras.
   * Stöd för Marketing Cloud Visitor-ID har lagts till.

* **Integration med Nielsen SDK**

TVSDK har nu stöd för att skicka mTVR- och MDPR ID3-beacons till Nielsen SDK utan någon anpassad integrering. För att komma igång hämtar du 3.1.2.19 Nielsen iOS App SDK och följer instruktionerna som finns i iOS Programmers Guide.

**Version 1.4.0**

* **Svart signalering med alternativ innehållsersättning**

Som en del av uppdateringen 1.4 TVSDK stöder nu även TVSDK att börja med och gå tillbaka från regionala strömavbrott mot linjärt innehåll. TVSDK kan nu bearbeta två manifestfiler parallellt, i huvudversion och alternativt, för att övervaka utpressningssignaler även när alternativ programmering visas i stället för den ursprungliga programmeringen.

* **Ta bort/ersätt C3-annonser**

Nu behövs inget ytterligare förberedelsearbete för att dynamiskt infoga nya annonser i VOD-resurser (video-on-demand) som kommer från C3-fönstret. TVSDK erbjuder nu ett API för att ta bort anpassade innehållsområden och dynamiskt infoga nya annonser. Den här kraftfulla nya funktionen är också användbar i fall där live/linjärt innehåll möts under sändning och omedelbart tas ned för användning som on demand-innehåll utan att man behöver ägna tid åt att&quot;rensa&quot; materialet.

## Lösta problem {#resolved-issues}

Där upplösning är kopplad till ett rapporterat problem visas en Zendesk-referens, till exempel ZD#xxxxx.

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 

-->

<!--
Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
-->

**iOS TVSDK 3.12**

* Direktuppspelningen misslyckas efter 15 minuters uppspelning när TVSDK används för iOS 3.10.

### Lösta problem i tidigare versioner {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998) - `isFallbackOnInvalidCreativeEnabled` orsakar att programmet kraschar.

* (ZD#41289) - `NSInvalidArgumentException` observeras med metoden `customParams` vilket leder till att programmet kraschar.

**iOS TVSDK 3.10**

(ZD#40943) - TVSDK-spelaren utlöser inte PTMediaPlayerStatusError-meddelanden när nätverket inte är tillgängligt.

**iOS TVSDK 3.9**

(ZD#40272) - iOS TVSDK kan inte spela upp VTT-undertexter med 101001-fel och leder till att appen låses.

**iOS TVSDK 3.8**

* (ZD#40087) - iOS kraschar med spelarfel för VOD-innehåll som har upphört att gälla.

* (ZD#40083) - Annonser före rullning spelas inte upp för boskap med `OpportunityGenerator` och spelaren ger ett felmeddelande.

* (ZD#39828) - `CurrentItem`-egenskapen saknar nullbarhetsanteckningen, vilket gör att spelaren kraschar när spelarstatusen i meddelandet är `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961) - Innehållet kan inte spelas upp i PiP-fönstret (Picture-in-Picture) när ett innehåll har spelats upp, när flera innehåll har konfigurerats för att spelas upp i PiP.

**iOS TVSDK 3.6**

Inga nya problem i den här versionen.

**iOS TVSDK 3.5**

Inga nya problem i den här versionen.

**Version 3.3**

(ZD#37820) - En lista över tillåtna för anpassat huvud-HS-ID, HS-SSAI-TAG har lagts till.

**Version 3.2**

* **Biljett#36588**  - En krasch inträffar när STOP-metoden för MediaPlayer anropas.

Korrigerad intermittent krasch som observerades när STOP-metoden anropades för några strömmar med undertexter.

* **Ticket#37080** - Dubblettbegäranden för manifestanrop visas.
Åtgärdade dubblettbegäranden som gjorts för manifest-URL:er under uppspelning. TVSDK gör nu ett anrop per manifest.

* **Biljett#37** - CRS-normaliseringsregel misslyckas med matchningstypen eq. Åtgärdat ett fall där spelaren kraschade när den påträffades med den senaste normaliseringsregeluppsättningen för värdnamn med matchningstypen &quot;eq&quot;.

**Version 3.1**

**Biljett nr 36313**  - Intermittenta oförutsägbara resultat vid linjär annonsuppspelning med fast intermittent uppspelning under linjära annonsuppspelningar i liveströmmen.

**Version 3.0.1**

**Biljett36948** - CRS - Inkonsekvent ordning för val av tillgångar i iOS 12 Den resurs som valts för CRS är inte alltid den högsta kvalitetsvarianten som returneras i ett VAST- eller VMAP-svar.

**Version 3.0**

* **Biljett35311** - Spelarstatus PAUSAS inte under ett avbrott i telefonsamtalet Tillagd avbrottshanterare för att stoppa spelaren från att avbrytas. Vid avbrott ändras spelarstatusen till PAUSED och uppspelningen återupptas när du klickar på uppspelningsknappen.

* **Biljett36685**  - Live-resurser - Tidsmatchningsfel med spelarens tidsförlopp och SCTE-markörtid Korrekt tid beräknas för SCTE-markörerna som ligger före direktpunkten.

* **Biljett36492** -  `currentTime` och  `localTime` uppdateras inte när du försöker till en ny position under den pausade statusspelarens aktuella tid kan nu anges till noll om spelaren är i pausat läge. tidigare var den aktuella tiden inställd på noll endast i uppspelningsläge.

**Version 1.4.45**

* **Ticket36294** - iOS TVSDK fungerar inte med Xcode 10 Åtgärdade kompileringsproblemen med TVSDK i XCode 10. På grund av XCode 10-kraven kräver appar som bygger på TVSDK för iOS 1.4.45 och framåt ett lägsta distributionsmål som iOS 7.0

* **Biljett36321**  - En diskrepans har observerats i sökbart intervall mellan  `PTMediaPlayer` och  `AVPlayer` instansen i läget&quot;Spelas upp&quot;.

* **Ticket36493** -  `libstdc++` stöd för iOS 12 Åtgärdade kompileringsproblemen med TVSDK på iOS 12. Appar som byggs på TVSDK för iOS 1.4.45 och framåt kräver lägsta distributionsmål som iOS 7.0

**Version 1.4.44**

* **Biljett34683**  - Förloppstiden för annonsuppspelning är negativ

Ytterligare kontroller har lagts in för att hantera fallet när det finns en avvikelse mellan den varaktighet som rapporteras av annonsservern och det faktiska annonsinnehållet.

* **Ticket34801** - currentTime och localTime uppdaterades inte vid sökning till en ny position under pausad status. Spelarens aktuella tid kan nu anges till noll om spelaren är i pausat läge. tidigare var den aktuella tiden inställd på noll endast i uppspelningsläge.

* **Biljett35037**  - Uppspelningen stoppas med felaktig URL vid återgång från signalbaserad annonsinfogning.
Förbättrad korrigering för stängda utgåvor nr 34385 i version 1.4.42. Tillagd isAvbruten kod för kontroll och undantagshantering för att göra åtgärdskön mer robust.

**Version 1.4.43**

* (ZD#32990) - iOS: Innehåll spelas upp i stället för annonser på vissa referenspunkter. `selectedMediaOptionInMediaSelectionGroup` API som ingick i AVPlayerItem-gränssnittet har nu flyttats under AVMediaSelection i iOS 11. Problemet löstes med det nya API:t.

* (ZD#33683) TVSDK borttaget == suffix från metadatasträngarna. Problemet har åtgärdats i tolkningslogiken.

* (ZD#33905) - iOS TVSDK anropar manifestfilerna med två användaragenter. Problemet med användaragenten har åtgärdats i första m3u8-anropet (fall av ny installation). M3u8 har samma användaragenter för alla samtal nu.

* (ZD#34293) - Förrullningar som infogats i LINEAR-strömmar spelas inte upp korrekt i iOS11. Problemet är åtgärdat för förhandsannonser.

* (ZD#34684) - När principen för att hoppa över annonser tillämpas visas bildrutor för förrullning i några sekunder. Ett nytt API, enableVodPreroll, har introducerats för att inaktivera uppspelning före videouppspelning. Standardvärdet för denna API är Yes. API:t gör att det inte går att sammanfoga annonsinnehåll i huvudinnehållet.

* (ZD#34765) - Efter att stop() anropats hämtas fortfarande få transportströmssegment. Förbättrade API:t Stop() för att undvika hämtning av de extra segmenten.

* (ZD#34865) - Annonser före registrering för djurbesättningar trunkeras på iOS. Relaterat till iOS11 och att lägga till ytterligare en kontroll för att bekräfta om strömmen är pre-roll eller main-content åtgärdar detta problem.

* (ZD#35093) - Korrigerade ett redundansscenario där uppspelningen inte växlar till säkerhetskopieringsströmmen om den primära varianten av strömmen misslyckas vid start (returnerar 404).

**1.4.42 (1.4.42.118)**

* (ZD#34385) - Uppspelningen stoppas med en felaktig URL vid återgång från signalbaserad annonsinfogning.

   Öka det maximala antalet samtidiga för `CustomAVAssetLoaderOperations` så att manifestläsningarna kan fortsätta att köras.

* (ZD#34373) - Slutanvändare kan inte direktuppspela till HDMI-anslutna enheter när direktuppspelningsinspelning inte tillåts.

* (ZD#32678) - TVSDK samlar inte in rätt annons-ID på iOS.

   Annons-ID för den slutliga annonseringen hämtas nu i VHL-pingar vid VAST-/VMAP-omdirigeringar.

* (ZD#33904) - TVSDK har inte registrerats för AVFoundation-meddelanden `AVAudioSessionMediaServicesWereLostNotification` och `AVAudioSessionMediaServicesWereResetNotification`.

   `PTMediaServicesWereLostNotification` och  `PTMediaServicesWereResetNotification` kan nu registreras i spelarappen för att få meddelanden när medietjänsterna återställs eller går förlorade.

* (ZD#33815) - Kunder kan inte uppdatera sina CRS-regler för prioritering och normalisering utan att behöva uppdatera appen.

   Lade till API:erna `getCRSRulesJsonURL` och `setCRSRulesJsonURL` i iOS TVSDK.

**Version 1.4.41 (1.4.41.76)**

* (ZD #34464) - Issues building Reference App with TVSDK Version 1.4.41

   Från och med den här versionen krävs Xcode 9 för kompilering av TVSDK för iOS.
* (ZD #29456) - Airplay startar i pausat läge

   Åtgärdade pausproblemet som uppstod när videon pausades när airplay startades.
* (ZD #30371) - Starttiden för AdBreak ändras när vi infogar mer än 2 annonser i linjär ström

   Korrigerade felet vid uppspelning av innehåll på Apple TV, vilket förhindrar uppspelning helt
* (ZD #32146)- Ingen `PTMediaPlayerStatusError` har tagits emot för HLS Live-innehåll vid blockering av iOS 11 dev beta

   Ingen `PTMediaPlayerStatusError` har tagits emot för HLS Live- och VOD-innehåll vid blockering med Charles (Drop connection and 403).

* (ZD #29242) - Airplay-videouppspelning misslyckas med annonser aktiverade.

   När annonser är aktiverade och AirPlay är aktiverat när du börjar spela upp en video, startar aldrig videouppspelningen och inget fel visas.

* (ZD#33341) - `DRMInterface.h` utlöser build-varningar i Xcode 9.

   Korrigerade två blockprototyper i `DRMInterface.h` som saknade ordet void i sina parameterlistor.

* (ZD#31979) - Kompilerar/körs inte när det är iOS 10 eller senare för iPhone 7/iPhone7+.

   Korrigerad kompilering av IB-dokument för tidigare versioner än iOS 7 stöds inte längre.

* (ZD#32920) - Tom skärm i en annonsbrytning och ingen annonsbrytning slutförs.

   När en annonsbrytning visar annonsförekomster och när en annonsförekomst är klar visas en tom skärm.

* (ZD#32509) - Inaktivera skärminspelning för iOS 11 Inaktivera skärminspelning för iOS 11.

* (ZD#33179) - Intermittent händelsefel i iOS11.

   Åtgärdade händelsefelet i iOS 11.

**Version 1.4.40** (1.4.40.72)

* (ZD #32465) - Spelaren kan inte hantera sammanfogade spellistor.

   Ring `finishLoadingWithError`(med: Fel) för AV-grund för att prova alternativa strömmar/utlösa failover.

* (ZD #31951) - TVSDK-fel under licensroteringar.

   Korrigerade licensrotationsproblemet.
* (ZD #31951) - Tom skärm i en annonsbrytning och ingen annonsbrytning slutförs.

   Hanterade ett problem där Facebook VPAID-annonser ofta returnerade flera CDATA-block i en enda VAST-nod.`<AdParameters>`
* (ZD #33336) - iOS TVSDK - Ad pods not be fill, trots att tillräckligt många annonser returnerades av Freewheel.

   Skapade en överordnad-underordnad relation mellan sekvensannons och reservannons och sortering baserat på överordnad sekvens och index.

**Version 1.4.39** (1.4.39.43)

* (ZD #32178) - iOS TVSDK-versionen är felaktig.

   TVSDK-versionen i loggfilerna var 1.0.211. Den är fast för att få rätt version.

* (ZD #32199) - Lazy Ad loading - Video visas inte för innehållet.

   Den lokala Adbreak-tidslinjen som inte initierades tidigare uppdateras nu innan den används.

* (ZD #27528) - Video, ljud eller båda fryser 1-45 sekunder efter att en resurs börjar spelas upp, om det sekundära ljudet är inställt på icke-standard iOS 1.2.

   Förbered och informera ljudspår i tillståndet Ready.

* (ZD #30411) - Du kan få oväntade resultat, t.ex. inget ljud eller felaktigt ljud, om du väljer ett sekundärt Sap-språk.

   Förbered och informera ljudspår i tillståndet Ready.

* (ZD #32199) - Lazy Ad loading - Video visas inte för innehållet.

   Den lokala Adbreak-tidslinjen som inte initierades tidigare uppdateras nu innan den används.

* (ZD #27528) - Video, ljud eller båda fryser 1-45 sekunder efter att en resurs börjar spelas upp, om det sekundära ljudet är inställt på icke-standard iOS 1.2.

   Förbered och informera ljudspår i tillståndet Ready.

* (ZD #30411) - Du kan få oväntade resultat, t.ex. inget ljud eller felaktigt ljud, om du väljer ett sekundärt Sap-språk.

   Förbered och informera ljudspår i tillståndet Ready.

**Version 1.4.38** (1.4.38.860)

* (ZD #29281) - iOS: Lägg till AdSystem och Creative Id i CRS-begäranden

Användning av kreativt ID och AdSystem i CRS-begäran baserat på CRS-normaliseringsregler

* (ZD #29176) - Krasch `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

Krasch på grund av tom AdBreak hanteras nu.

* (ZD #30125) - Programmatiska annonser fungerar inte på iOS-plattformen

Stöd för programmatiska annonser i iOS har lagts till.

* (ZD #30782) - #EXT-X-PROGRAM-DATE-TIME Notification

Timed metadata-händelse utlöses inte för taggen # EXT-X-PROGRAM-DATE-TIME med LIVE-DRM-strömmar.

**Version 1.4.37 (1.4.37.842)**

* (ZD #28950) - Problem med VOD-uppspelning

Uppspelningsproblem när taggen # EXT-X-PLAYLIST-TYPE i strömmen är inställd på Event i stället för VOD

* (ZD #29281) - iOS: Lägg till AdSystem och Creative Id i CRS-begäranden

Användning av Creative Id och AdSystem i CRS-begäran baserat på CRS-normaliseringsregler.

* (ZD #29462) - TremorHub-annons i A&amp;E VOD orsakar en krasch i iOS-appar

**Version 1.4.36 (1.4.36.835)**

* (ZD #29418) - Cues med varaktighet 0 (#EXT-X-CUE-OUT:0.000) gör att iOS TVSDK stoppar eller kraschar uppspelningen.

Problemet är åtgärdat och uppspelningen startar korrekt.

* (ZD #29462) - Annons i VOD orsakar en krasch på iOS TVSDK.

Problemet är åtgärdat. iOS TVSDK genererar ett `exception(AUDNetworkAdInfo::initWithAdId)`-värde och hanterar det inte. Undantaget beror på ett tomt ID.

* (ZD #29281) - Lägg till AdSystem och Creative ID i CRS-begäranden.

Inkludera AdSystem och CreativeId som nya parametrar i förfrågningarna 1401 och 1403 (alla andra parametrar är desamma).

**Version 1.4.35** (1.4.35.830)

* (ZD #27830) - Måste programmässigt avgöra skillnaden mellan undertexter och undertexter i iOS.

TVSDK visar nu de två typerna som kan användas för att filtrera ut den bildtexttyp som krävs.

* (ZD #29160) - EXT-X-CUE-OUT ad ad cues är inte korrekt indelade på iOS med TVSDK.

EXT-X-CUE-OUT-mikrofon spelas nu upp.

* (ZD #29100) - Programmet kraschar när användaren drar till slutet av en film.

Flera krascher relaterade till synkronisering har korrigerats.

* (ZD #28785), (ZD #27712) och (ZD #25076) - iOS-appen kraschar under de stora livehändelserna.

Flera krascher relaterade till synkronisering har korrigerats.

**Version 1.4.34** (1.4.34.815 för iOS 6.0+)

* (ZD #28481) - FER-avbrott på grund av att fel tangent läggs till i slutet av en annonsbrytning för dessa FER-strömmar

För en FER-ström infogas nyckeln före annonsbrytningen efter slutet av annonsbrytningen. Problemet löstes genom att den *senast visade nyckeln* lades till i slutet av annonsbrytningen.

**Version 1.4.33** (1.4.33.803 för iOS 6.0+)

* (ZD# 21701) Aktivera CRS för underkonton

Aktiveras genom att den ursprungliga kreativa URL:en för 1401 CRS-begäran skickas i stället för den normaliserade URL:en, enligt kravet för CRS back end.

* (ZD# 26218) - PSDKResources.bundle loading issue

Problemet löstes genom att resursinläsningen uppdaterades för att se från alla tillgängliga paket.

* (ZD# 27460) Midroll first Ad call - POST to `cdn.auditude.com` return 403.

Det nya CDN-kontot kan inte hantera en CDN-begäran för POST. Problemet löstes genom att koden uppdaterades så att annonsbegäran `cdn.auditude.com` blev GET istället för POST.

**Version 1.4.32** (1.4.32.792 för iOS 6.0+)

* (ZD# 27132) Stöd för decimalvärden för VMAP-annonsbrytningar.

När innehåll inte segmenterades längs de definierade annonsbrytningarna orsakade heltal oväntade annonsplaceringar. Problemet löstes genom att decimalvärdena inte konverterades till heltal.

* (ZD# 27189) AES-innehåll med taggen EXT-X-DISCONTINUITY-SEQUENCE spelas inte upp korrekt.

Problemet löstes genom att taggen placerades i början av spellistan.

**Version 1.4.31** (1.4.31.785 för iOS 6.0+)

* (ZD# 24528) Implementera TVSDK-användningsstatistik för fakturering

Mer information finns i [Faktureringsmått].

* (ZD# 24642) Stöd för bild-i-bild för TVSDK

Bild-i-bild-funktionen, som i vissa fall inte fungerade korrekt, har åtgärdats.

* (ZD# 25246) Felaktiga brytningssignaler

Problemet löstes genom att sammanföra diskontinuitetstaggar i olika variantmanifest.

* (ZD# 26218) Programbyggprocessen blir komplicerad när PSDKLilibrary.framework ska inkluderas i klientens programramverk

Problemet löstes genom att paketet PSDKLilibrary.framework paketerades enligt begäran.

* (ZD# 26364) Multi-CDN-stöd för CRS-annonser

Mer information finns i Multiple CDN-stöd för CRS-annonsleverans.

* (ZD# 27028) Fördröjning vid uppspelning av vissa strömmar i iOS 10.

Problemet löstes genom en tillfällig lösning för strömmar som inte har ett M3U8-tillägg.

**Version 1.4.30** (1.4.30.754 för iOS 6.0+)

Följande problem löstes för TVSDK i den här versionen:

* (ZD# 24180) Lägg till en anpassad rubrik i tillåtelselista.

En ny anpassad rubrik har lagts till i TVSDK tillåtelselista.

* (ZD# 25016) Redundansström väljs slumpmässigt när ABR-kontrollparametrar anges

Problemet löstes genom att ABR-strömmarna bibehölls i ordning när ABR-inställningarna medföljer inställningen initialBitrate för en ström som innehåller URL:er för växling vid fel. Detta undviker att spela upp redundansströmmarna i stället för primärströmmarna.

* (ZD# 25076) Krasch på PTAuditudeAdResolver loadComplete

Problemet där en krasch inträffade vid snabb start/stopp av flera PTMediaPlayer-instanser med annonser har åtgärdats.

* (ZD# 25960) Inga fler prenumerationstaggar utlöser utsändningar av meddelanden om metadataändringar

Problemet där en prenumerationstagg inte meddelas när den visas innan det första segmentet i manifestet har korrigerats.

* (ZD# 26084) PSDK som ger 106000.101000.-11833 Det gick inte att hitta något fel vid övergång från den senaste annonsbrytningen till underhållningsinnehåll

När den sista starttiden för en annonsbrytning från VMAP infaller innan den totala längden är slutförd, infogas i vissa fall inte nyckeln förrän efter slutet av den sista annonsbrytningen. Problemet har åtgärdats.

* VHL (Video Heartbeat Library) har uppdaterats till version 1.5.9 för att lösa följande problem:

* (ZD #22351) VHL - Analys: Varaktighet för livevideoresurs

Problemet löstes genom att ett objekt-Duration-API lades till i PTVideoAnalyticsTrackingMetadata för att uppdatera resursens varaktighet för live-/linjära strömmar och tillhandahålla en logik för att kontrollera liveströmmen.

* (ZD# 22675) VHL - Analys: Uppdaterar livevideoresursens varaktighet

Problemet är detsamma som ZD #22351.

* (ZD #25908) VHL - Analys: Händelsekrasch för pulsslag i Adobe

Problemet löstes genom att implementeringen uppdaterades för att använda den senaste versionen av VHL för iOS version 1.5.9 för att förbättra stabilitet och prestanda.

* (ZD #25956) VHL - Analys: Krasch vid upprepad uppspelning av videoklipp

Problemet är detsamma som ZD #25908.

**Version 1.4.29** (1.4.29.743)

* (ZD# 23901) Annonser från tredje part spelas inte upp

Problemet löstes genom att URL-strukturen för CRS v3 flyttades så att zon-ID inkluderades i den ompaketerade URL:en.

* (ZD #25183) Problem med DRM-uppspelning på tvOS och iOS

Problemet löstes genom stöd för flera nyckeltaggar som behövs för stöd av flera DRM.

* (ZD# 25334) TVSDK kan inte spela upp ett delat cDVR-innehåll

Problemet löstes genom att TVSDK inte kunde konvertera tomma strängar till absoluta URL:er.

* (ZD# 25347) Ange anpassad HTTP-rubrik för AVURLAsset

Stöd har lagts till för anpassade rubriker i segmentbegäranden via klassen PTNetworkConfiguration.

**Version 1.4.28** (1.4.28.722)

* (ZD #24549) Flera annonseringsanrop

Problemet löstes genom att tidslinjehanteraren uppdaterades för att lyssna efter meddelanden på ett specifikt objekt när flera spelare skapades.

* (ZD #24758) PTManifestLogger stöder inte iOS 8

Problemet löstes genom att logger-verktygsbiblioteket uppdaterades till distributionsmålet version 7.0.

* (ZD #24775) Fördröjd ström på grund av annonser

Problemet löstes genom korrekt beräkning av varaktigheten i händelsespellistor.

* (ZD #24799) Vissa avsnitt spelas inte upp i iOS APP

Problemet löstes genom att den lokala webbservern användes för undertexter när WebVTT-filerna är geografiskt begränsade.

**Version 1.4.27** (1.4.27.711) för iOS 6.0+

* (ZD #24089) - Optimeringar för annonsupplösning på långa DVR-strömmar

Problemet löstes genom att flera optimeringar lades till för att minska den tid som krävs för att bearbeta DVR-fönstret i live/linjära strömmar.

* (ZD #21554) - felfyrar i TVSDK som inte utlösts för programtypen = video/mp4

Problemet löstes genom att spelaren aktiverade att pinga rätt URL för felspårning i ogiltiga resursformat.

* (ZD #24424) - Krascher av typen EXC_BAD_ACCESS KERN_INVALID_ADDRESS har sitt ursprung i PSDKLib för iOS på senare maskinvaruenheter.

Kraschen som inträffade på grund av en icke allokerad mediespelarinstans, när uppspelningen växlas snabbt mellan olika strömmar, har åtgärdats.

* (ZD #24575) - Krasch i TVSDK på 32-bitarsenheter när enableDebugLog=true

Problemet med loggformatet som orsakade kraschen på 32-bitarsenheter när loggning är aktiverat har åtgärdats.

**Version 1.4.26** (1.4.26.702) för iOS 6.0+

* (ZD# 20213) - TVSDK FW måste vara dynamiskt/modulariserat för XCode7

Åtgärdat genom att uppdatera biblioteken med modulstöd

**Version 1.4.25** (1.4.25.684) för iOS 6.0+

* (ZD #19629) - Live Video Pauses when Entering Airplay to ATV 4

Problemet löstes genom att en vänteperiod lades till efter att gamla objekt tagits bort, men innan nya objekt lades till i AVQueuePlayer. Utan vänteperioden skickas meddelanden till fel objekt.

* (ZD #19856) - Inga undertexter visas när de är aktiverade som standard

Problemen i webbspellistan, som fick undertexterna att inte visas korrekt, har åtgärdats.

* (ZD #21590) - Videoprestanda och -spårning i Senaste origin-byggen

Problemet med att videolängden saknas i VideoAnalytics har åtgärdats.

* (ZD #20202) - iOS-appen kraschar om du anger anpassade undertextningsformat

Problemet löstes genom att ytterligare null-objektkontroller lades till när underrubriksformat angavs.

* (ZD #20709) - videolängden rapporteras som 0 i spårning av videostart

Problemet är detsamma som (ZD #21590).

* (ZD #22280) - Analytics-videolängd anges till 0

Problemet är detsamma som (ZD #21590).

* (ZD #22592) - Problem med Airplay i Primetime

Problemet är detsamma som (ZD #19629).

* (ZD#22922) - Manuell växling av bithastighet för iOS

Problemet löstes genom att ett alternativ angavs för den maximala bithastigheten.

* (ZD #23084) - Apple-kompatibilitet för nätverk med endast IPv6

Symbolerna som inte rekommenderas av Apple för IPv6-kompatibilitet har tagits bort.

**Version 1.4.24** (1.4.24.661) för iOS 6.0+

* ZD #2548) - Primetime-stöd för interaktiv annonsering på mobilen - VPAID 2.0

Problemet löstes genom att logiken uppdaterades för att visa spelarvyn om en VPAID-annons inte kan spelas upp.

* (ZD #20101) - Anpassad kapitelimplementering startar kapitelstarthändelse under annonsuppspelning

Problemet löstes genom att VideoAnalyticsTracker uppdaterades för att korrekt identifiera inledande/slutförande av kapitel vid övergång mellan kapitelgränser och icke-kapitelgränser.

* (ZD #20784) - Analys: Utlösande av innehåll för live-videoövergångar

Problemet löstes genom att en logik lades till för att manuellt aktivera slutförandet av innehåll under en videospårningssession.

Följande bibliotek uppdaterades:

* AdobeMobile-bibliotek till 4.10.0
* VHL-bibliotek till 1.5.6
* Biblioteket VHL-Nielsen till 1.6.7
* (ZD #21855) - Undertexter spelas inte upp efter mittrullen

I det här problemet orsakade duplicerade diskontinuitetstaggar att undertexter inte skulle visas efter mittrullen. Problemet löstes genom att ta bort de diskontinuitetstaggar som finns bredvid varandra.

* (ZD #21994) - Sträng utanför gränserna i PTHLSUtils

Den troligaste orsaken till kraschen är när en EXT-X-KEY har en URL som omges av citattecken.

* ZD #22074) - AUDVAST krasch inträffar en gång i minuten på iOS

I version 1.4.23 har kraschen som orsakades av osäkra tecken i en VAST-omdirigerings-URL åtgärdats. TVSDK fortsatte dock att hoppa över dessa annonser.

Problemet löstes genom hantering av osäkra tecken och genom att annonserna kunde spelas upp.

* (ZD #22694) - PTMediaPlayer.  Vyn är dold av spelaren

Problemet löstes genom att logiken uppdaterades för att visa spelarvyn om en VPAID-annons inte kan spelas upp.

**Version 1.4.23** (1.4.23.641) för iOS 6.0+

* (ZD #18016) - Inget svar från Primetime SDK med dåligt nätverkstillstånd

Problemet löstes genom att felmeddelanden förbättrades när ett allvarligt fel från AVFoundation inträffar och programmet kunde hantera omstarten efter felet.

* (ZD #20580) - Krasch i PTSplicerManager

Problemet löstes genom att ge ytterligare skydd mot samtidiga problem som orsakar kraschen.

* (ZD #21782) - iOS-felkod 10100

Problemet där TVSDK returnerade ett 101000-fel när uppspelningen av DRM-strömmar i Adobe Access har åtgärdats.

* (ZD #21889) - Uppspelning av onlineannonser och offlineinnehåll misslyckas

Problemet där uppspelningen misslyckades efter att en annons på AES-krypterat offlineinnehåll har korrigerats.

* (ZD #22074) - AUDVAST krasch inträffar en gång i minuten på iOS

Problemet löstes genom att hanteringen av VAST-annonstaggar från tredje part med ogiltiga tecken i URL:en förbättrades.

* (ZD #22257) - TVSDK kan inte spela upp DRM-strömmen

Problemet där TVSDK som returnerade ett 101000-fel när uppspelningen av DRM-strömmar för Adobe Access har åtgärdats.

**Version 1.4.22** (1.4.22.627) för iOS 6.0+

* (ZD #18709) - Krasch i TVSDK för iOS

Problemet med en krasch som inträffar på vissa DRM-skyddade dataströmmar med Adobe Access har åtgärdats.

* (ZD #18850) - Uppdatera logik för kreativt urval baserat på CRS-regler

Problemet löstes genom att en JSON-konfigurationsfil lades till för att ange prioritet för det kreativa urvalet.

* (ZD #19770) - Skyddad AES-videoutgång spelas inte längre

Problemet med att vissa 302 omdirigerade strömmar inte kunde spelas upp har åtgärdats.

* (ZD #19629) - Live Video Pauses when Entering Airplay to ATV 4

Problemet löstes genom att man lade till en lösning för live-videopaus när airplay är aktiverat för Apple TV 4-enheter. Problemet verkar vara en AppleTV 4-utgåva.

* (ZD #21119) - TVSDK stoppas efter annonsuppspelning

Stöd har lagts till för AES-krypterade strömmar med sekvens IV när annonsinfogning används.

* (ZD #21125) - Återgå från live/linjär och brytning tidigt

Stöd har lagts till för att gå tillbaka från en annonsbrytning tidigt innan annonsbrytningen spelas upp tills den är klar. Tidig retur anges med en anpassad manifesttagg.

* (ZD #21224) - Airplay-stöd för tokeniserade strömmar från Akamai

API:er har lagts till i klassen PTNetworkConfiguration för att lägga till cookies som URL-parametrar i segment för vissa tokeniserade Akamai-strömmar.

* (ZD #21287) - Överflödig logg

Ett problem med vissa loggsatser som visas som standard i xcode-konsolen har korrigerats även när loggning är inaktiverad.

* (ZD #21446) - Ad Break-händelser aktiveras ibland inte av TVSDK

I EVENT-strömmar aktiveras annonsbrytningar inte korrekt i den tidigare versionen. Den här versionen åtgärdar det här problemet.

**Version 1.4.21** (1.4.21.605) för iOS 6.0+

* (ZD #20749) - Återställning hoppar över VAST-svar som inte är tomma. Extra URL-adresser för annonsspårning

Ett problem med dubblettping på reservannonser har lösts.

**Version 1.4.20** (1.4.20.590) för iOS 6.0+

* (ZD #18639) - TVSDK använder för mycket processorkapacitet/resurser på en lång het-inspelningsresurs

Överdriven processoranvändning/resursanvändning har fastställts på två nivåer. Först genom att låta tidsuppdateringsfunktionen köras på en global kö i stället för på huvudtråden och genom att optimera CPU-användningen för att analysera manifestet med den tidigare bearbetade och cachelagrade m3u8.

* (ZD #19349) - Annonser före rullning hoppas över när nätverksanslutningen stryps.

Problemet löstes genom att en timeout-händelse (requestTimeout) angavs för programmet och i adMetadata.  adRequestTimeout API för att åsidosätta standardtidsgränsen på 10 sekunder.

* (ZD #19446) - Meddelande saknas i liveströmmar

Problemet löstes genom att programmet tilläts prenumerera på EXT-X-PROGRAM-DATE-TIME på liveströmmar.

* (ZD #19459) - Krasch vid förberedelse av alternativt ljud med PTMediaPlayerItem prepareAudioOptionsWithAVMediaSelectionOptions
* (ZD #19460) - Krasch - `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

Problemet är detsamma som Zendesk #19459.

* (ZD #19574) - TVSDK returnerar inte M3U8-svarsdata för DRM- eller icke-DRM-innehåll

I den initiala inläsningen av manifestfilen i PTMediaPlayerItem.prepareToPlay rapporterar inte TVSDK brödtexten för felsvaret på programmet om det inte gick att läsa in manifestet.

Problemet löstes genom att TVSDK fick rapportera felsvaret som ett fel till programmet.

* (ZD #19615) - Återställningslogiken fungerar inte

I den aktuella implementeringen hoppades reservannonser över och packades inte om såvida inte dessa annonser är i m3u8-format. Problemet löstes genom att även stödet för ompaketering av reservannonser lades till.

* (ZD #19770) - TVSDK kan inte spela upp skyddat AES-innehåll med 302-omdirigering

Omdirigeringsproblemet har åtgärdats eftersom omdirigerings-URL:en rensades av clearConnectionData innan den kunde användas för att analysera manifestet.

* (ZD #19856) - Undertexter visas inte för vissa bithastigheter när de är aktiverade som standard

Problemet löstes genom att felet från iOS hanterades för de segment i strömmarna där undertexterna inte visas.

* (ZD #19868) - TVSDK kraschar när en ogiltig kreatör handlas

Kraschen i TVSDK som felaktigt avallokerade en instans av den stora parsern har åtgärdats.

* (ZD #20180) - VPAID-annonser hoppas över ibland

JavaScript Mime-typen inkluderades inte alltid eller ansågs vara en giltig MIME-typ. Problemet löstes genom att JavaScript inkluderades som en giltig MIME-typ.

* (ZD #20749) - Återställning hoppar över VAST-svar som inte är tomma. Extra URL-adresser för annonsspårning

Problemet med att en del kreatörer inte packas om har åtgärdats.

**Version 1.4.19** (1.4.19.563) för iOS 6.0+

* ZD #18639) - TVSDK använder mycket processorkapacitet/resurser på en lång het inspelningsresurs

Problemet löstes genom att DRM m3u8-spellistan optimerades så att den skrivs om till cachelagrade bitar av spellistan som tidigare har skrivits om. Detta är mest relevant när du spelar upp live m3u8-strömmar för vilka m3u8 laddas ned efter varje segmentnedladdning.

* (ZD#18956) - player.drmManager är noll när brytpunkten anges i iOS Demo Player

Problemet löstes genom att implementeringen av API:t PTMediaPlayer.drmManager uppdaterades för att hämta DRMManager från DRM-ramverket.

**Version 1.4.18** ( 1.4.18.557) för iOS 6.0+

* (ZD #18844) Spåra spelhuvudet för direktinnehåll i iOS-spelaren.

Problemet löstes genom att programmet fick ange ett eget spelhuvudsvärde.

* (Zendesk #18518) - Om videonamnet inte anges blir TVSDK:s namn som standard * PSDK-baserad spelare.*

Problemet löstes genom att standardvärdet för spelarens namn togs bort.

**Version 1.4.17** (1.4.17.545) för iOS 6.0+

* (Zendesk #2228) - Förbättra TVSDK för att returnera JSON-svar från hämtning av ett manifest

I stället för att skicka ett fel när innehållet inte är M3U8, returnerar DRM Framework noll DRMMetadata. Problemet löstes genom att metadata lades till för att visa innehåll när M3U8_PARSER_ERROR-meddelandet inträffar.

* (Zendesk #2231) - Ett fel returnerades från hämtning av manifestet som inte är tillgängligt i MediaPlayerNotification

Samma upplösning som Zendesk #2228

* (Zendesk #3304) - VAST 3.0 `[ERRORCODE]`-makrot fylls inte i

Problemet där Auditude SDK inte kan skicka ett ping när spårnings-URL:en har blanksteg i början har åtgärdats.

* (Zendesk #17294) - Crash SecKeyRawSign

En eventuell krasch när kundens kod använder nyckelkedjan har lösts.

* (Zendesk #18008) - Stöd för cookies för iOS8+ för tokeniserade strömmar

Akamai-tokeniserade strömmar kräver att cookies skickas vid segmentbegäranden, vilket inte var möjligt i iOS 7 och tidigare. Från och med iOS 8 har Apple lagt till ett API som tillåter att cookies skickas för segmentbegäranden. Detta stöd finns nu i TVSDK. Stöd har också lagts till för att skicka en användaragent, om tillgängligt.

* (Zendesk #18166) - TVSDK 1.4.15 ger hundratals varningar vid kompilering med DWARF med dSYM-filalternativ

Alla varningar har åtgärdats.

**Obs**: tvOS-kompatibla bibliotek har lagts till för TVSDK.

**Version 1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S kraschar vid uppspelning

Återställer surfHTTP-beroendet för CRS eftersom TVSDK nu använder httpurlconnection i stället för curl. Problemet löstes genom att undantagen rensades innan ett nytt JNI-anrop gjordes.

* (Zendesk #4487) - Spårning av innehållets linjära kanal

Problemet löstes genom ominitiering av spåraren för pulsslag i videon under en linjär direktuppspelningssession.

* (Zendesk #17919) - Android - innehållssökning orsakar hjärtslagsfel

Problemet var att lösa pulsslag i ett feltillstånd när det finns en sökning i ett kapitel

* (Zendesk #18053) - Program som använder TVSDK kraschar på Marshmallow

TVSDK kraschade i Android M OS när TSDK-biblioteket använder neonkod som gör YUV `->` RGB-färgkonvertering. Problemet löstes genom att funktionerna som orsakar problemet uppdaterades med en icke-neon version av `code`.

* (Zendesk #18072) - Android M - Application Crash

Den här kraschen inträffar när API:erna MediaCodecList och MediaCodecInfo anropas när profilen och nivån kontrolleras. Adobe söker Googles stöd för ytterligare insikter. Problemet löstes genom att en temporär lösning skapades genom att all kodekinformation lästes in i förväg för att undvika att anropa dessa API:er endast när kodekinformation behövs.

* (Zendesk #18074) - Arabiska undertexter som inte fungerar på Nexus med Android 6.0

Problemet löstes genom stöd för teckensnittskartan i Android CTS.

**Version 1.4.15** (1.4.15.512) för iOS 6.0+

**Obs**: Nielsen-modulen har tagits bort från TVSDK-bygget, men TVSDK kommer att uppdateras inom den närmaste framtiden med en ny Nielsen-integreringsmodul.

* (ZD #2228) - Ett fel returnerades när manifestet hämtades som inte är tillgängligt i MediaPlayerNotification

Lagt till metadata för att visa innehåll när meddelandet M3U8_PARSER_ERROR inträffar.

* (ZD #4437) - kraschar i Adobe Primetime SDK

Korrigerade en rapporterad krasch vid förberedelse av undertexter/alternativt ljud.

* (ZD #4487) - Spårning av innehållets linjära kanal

Tillåts ominitiering av spårningsfunktionen för pulsslag under en linjär direktuppspelningssession.

**Version 1.4.14** (1.4.14.498) för iOS 6.0+

* (ZD #17260) - Krasch i playlistManagerForURL

Korrigerade en intermittent krasch på grund av samtidighetsproblem.

**Version 1.4.13** (iOS 6.0+)

* (ZD #3304) - VAST 3.0 `[ERRORCODE]`-makrot fylls inte i

   * Felkod 400 visas om den är infogad   och har dålig kreativitet.
   * `[ERRORCODE]` makrot kommer att URL-kodas.

* (ZD #3865) Integrering av pulsslag med IMA-annonser

Korrigerade ett fel där videolängden rapporterades felaktigt.

* TSDK-demospelaren för iOS 9 har uppdaterats

För att ha korrekt stöd för iOS 9 måste du konfigurera undantagen i Application Transportation Security. I syfte att genomföra demonstrationen är ATS helt inaktiverat.

**Version 1.4.12** (1.4.12.464) för iOS 6.0+

* (ZD #4521) CRS Testing Client Side och SSAI

Korrigerat felaktig omvänd MD5 i 3P-URL.

**Version 1.4.12** (1.4.12.463) för iOS 6.0+

* (ZD #2751) CSAI and CRS / Förbättra: Hantera dynamiska element i vissa URL-adresser för mediefiler.

Uppdaterad Creative Repackaging Service för att hantera annonser med dynamiska kreativa URL:er.

* (ZD #3654) Minnesläcka i PSDK-version efter 1.3.4.166

Korrigerat minnesläckage i drmFramework med normal uppspelning på iOS 8.2-enheter

* (ZD #3988) Förhandsgranskning hoppas över vid återsökning efter första uppspelningen

Korrigerade ett fel så att annonsprinciper kunde inaktiveras korrekt.

* (ZD #4017) Begär att iOS-API ska tvinga annonsuppspelning på bakåtriktad sökning

Löst med fix för ZD #4279

* (ZD #4279) HLS TVSDK ad insertion -302 redirect issue on iOS and Desktop

Ett fel har korrigerats när en annonsresurs använde en relativ omdirigerings-URL

**Version 1.4.9** (1.4.9.427) för iOS 6.0+

* (ZD #3075) Problem med att nå Internet - iOS

Meddelande har lagts till för att identifiera när uppspelningen har avstannat.

* (ZD #3193) Begäran om ett API för profiländring i TVSDK

PTPlaybackInformation har uppdaterats för att visa den uppdaterade versionen av IndicateBitrate. BITRATE_CHANGE-meddelandet har uppdaterats för att vara mer tidstillförlitligt och korrekt jämfört med M3U8-rapporterade bithastigheter.

* (ZD #3324) Primetime-annonser rapporterar problem när inga annonser finns i VMAP

Stöd för pingning av tomma URL:er för annonsspårning. TVSDK kommer nu att verifiera start av annonsbrytning och slutföra pingning för tomma annonsbrytningar.

**Version 1.4.8** (1.4.8.402)

* (ZD #3158) IOS 7 kraschar vid repriser av fullständiga händelser

**Version 1.4.7** (1.4.7.382)

* (ZD #2197) Spårning och fel. Det gick inte att läsa in manifestet för det tillagda meddelandet för resursen.
* (ZD #2894) Spelaren gör fyra manifestbegäranden på högsta nivån under uppspelning.
* (ZD #2992) Auditude Rapporterar konstiga varaktigheter och identifierare.

**Version 1.4.6**(1.4.6.325)

* (ZD #2197) Spårning och fel. Tillagda meddelanden för resursen kunde inte läsa in manifestet

**Version 1.4.5** (1.4.5.283)

* (ZD #2141) Analysimplementering för TreeHouse-appen, lade till biblioteket `AdobeAnalyticsPlugin.a` för att skapa paketet.
* Video Heartbeats Library update to 1.4.1.2
* (PTPALY-4226) (relaterat till ZD #2423) Om du utför DRM-återställning kan programdokumentdata tas bort.

**Version 1.4.4** (1.4.4.242)

* Video Heartbeats Library (VHL) update to 1.4.1.

* (ZD #2435) TV SDK-dokumentation om uppdateringar av analysbehov

**Version 1.4.2** (1.4.2.210): iOS 6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` returnerar tomt
* (ZD #2109) Primetime PSDK 1.4.1.125 fungerar inte med Xcode 5.1.1
* (ZD #2137) Krasch i PSDK på iOS när DRM-metadata inte kan läsas in

**Version 1.4.1**(1.4.1.125)

* (ZD #1107) CocoaLumberjack - duplicerade symboler
* (ZD #1644) Ändra iOS-användaragent för målgruppsanpassning och rapportering
* (ZD #1850) Cocoa Lumberjack-filer som ingår i iOS SDK
* (ZD#1908) Anpassade taggar ignoreras av PSDK om det finns fler än 1

**Version 1.4.0** (1.4.0.32)

* Zendesk #1024 - Funktion för att ta bort annonser från strömmen via manifest

## Enhetscertifiering och stöd för {#device-certification-and-support}

>[!NOTE]
>
>Följande funktioner stöds **inte** i TVSDK:
>
>* Långsam rörelse, oavsett plattform eller version.
>* Livetrick.


**Version 1.4.43**

* TVSDK 1.4.43 är certifierat för iOS 11.

**Version 1.4.29**

* TVSDK 1.4.29 har certifierats för iOS 10.

**Version 1.4.28**

* TVSDK 1.4.28 har certifierats för iOS 10 Beta 7.
* DRM-stöd för att tvinga HTTPS genom att lägga till API:er för `forceHTTPS` och `isForcingHTTPS`.
* VHL-bibliotek har uppdaterats till 1.5.8, Adobe Mobile-bibliotek till 4.8.4 och loggningsverktygsbiblioteket till version 7.0-distributionsmålet.

**Version 1.4.19**

Den här versionen av TVSDK har certifierats med FairPlay-stöd för iOS och tvOS.

**Version 1.4.17**

* tvOS

   Den här versionen av TVSDK har stöd för tvOS och har certifierats för okrypterade HLS-strömmar.

   **Obs**: Kom ihåg följande riktlinjer för kompilering:

   * Stödet för tvOs i TVSDK är begränsat till DRM-krypterade strömmar som inte är Adobe. Du måste ta bort referensen till drmNativeInterface.framework i inställningarna för tvOS-bygget. AES-krypterade strömmar stöds fortfarande.
   * Apple kräver att alla Apple TV-program är bitkodsaktiverade, så du måste aktivera den här flaggan i dina projektinställningar.

## Kända fel och begränsningar {#known-issues-and-limitations}

* På grund av borttagning av klassen iOS UIWebView i iOS TVSDK 3.6 och senare:
   * VPAID-annonser spelas inte upp som förväntat i iPad 13.
   * Pressannonser kommer inte att spelas upp som förväntat.

* I iOS TVSDK sammanfogas alla annonser i innehållsmanifestet. Annonsbeteenden implementeras genom att söka baserat på innehållets och annonssegmentens varaktighet. Så om segmentens varaktighet inte är korrekt kanske sökningen inte alltid avslutas vid den exakta bildrutan i början eller slutet av annonsbrytningen. Även om varaktigheten är för bildrutan finns det en tolerans som plattformen själv tillämpar på sökning och det kan finnas några ramar, annonser eller innehåll som visas. Detta är en begränsning av plattformen och hur annonsinfogning fungerar med TVSDK på iOS.
* Beslutet att hoppa över inträffar för seek-händelsen i det här fallet. Men eftersom längden på annonssegmentet i manifestet inte representerar annonsens faktiska längd korrekt, är sökningen inte korrekt. Därför visas några bildrutor med annonser när annonspolicyer tillämpas.
* Det kan hända att licensrotationsvideo inte spelas upp på iOS 11 och att den spelas upp korrekt på iOS 9.x och iOS 10.x.
* Om uppspelningen är aktiv över AirPlay hoppas VPAID-annonser över i VPAID 2.0-stödet.
* drmNativeInterface.framework länkar inte korrekt när minimimålet är iOS7 (eller senare).
Tillfällig lösning: Ange uttryckligen biblioteket libstdc+.6.dylib enligt följande: Gå till Mål->Bygg faser->Länka binärt med bibliotek och lägg till libstdc++.6.dylib.
* Det gick inte att infoga post-roll för ersättnings-API.
* Om du söker efter en annonsbrytning (utan att komma ut ur den) utfärdas en dubblett av meddelanden om annonsstart och annonsbrytningar
* Inställning av currentTimeUpdateInterval har ingen effekt.
Obs! I vissa iOS-versioner läser operativsystemet inte in resurserna i PSDKLilibrary.framework automatiskt. Det är viktigt att manuellt kopiera PSDKResources.bundle till programmets paketresurser: Gå till&quot;Bygg faser&quot; och kopiera paketresurser.
* Referensappen kan inte byggas med Xcode 8 eller tidigare versioner. iOS TVSDK version 1.4.41 och senare, använd Xcode 9 för att kompilera.
* VPAID-annonser respekterar inte värdet delayAdLoadingTolerance.
* 24077 - För visst HLS-innehåll med underrubriker kraschar spelaren vid metoden Stopp eller Återställ.
* Detaljerade felmeddelanden är inte tillgängliga om bara in Time Ad Resolution är aktiverat.
* Felmeddelanden loggas enligt annonsupplösningstiden och inte enligt annonssekvensen.
* HEVC-stödet har följande begränsningar i den här versionen
   * DRM stöds inte
   * Stöd för CC (CEA 608/708) är inte tillgängligt eftersom det inte stöds i CMAF.
   * 4K-stöd finns ännu inte.
   * ID3-taggar stöds inte eftersom det inte stöds i CMAF.
   * Omultiplicerade Live HEVC-strömmar har inte verifierats.
   * Stöd för HEVC-annonser har inte verifierats.
* När JIT är aktiverat och toleransen är inställd på 10 sekunder visas inget VAST-anrop för den första fabriken och fel vid VMAP->VAST-omdirigeringsannonser.
* För att tidsgränsen för annonsupplösningen ska fungera korrekt förväntar sig spelaren en sammanslagen spellista inom 20 sekunder varje gång spellistan uppdateras under direktuppspelning. Om den inte får en sammansatt spelningslista inom det angivna intervallet genereras ett internt fel och spelaren stoppas.

## Användbara resurser {#helpful-resources}

* [TVSDK 3.4 for iOS Programmer&#39;s Guide](https://docs.adobe.com/content/help/en/primetime/programming/tvsdk-3x-for-ios/introduction/ios-3x-overview.html)
* [API-referens för TVSDK iOS 3.4](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* Läs den fullständiga hjälpdokumentationen på [Adobe Primetime Learn &amp; Support](https://helpx.adobe.com/support/primetime.html)-sidan.
