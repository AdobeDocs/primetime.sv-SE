---
title: Versionsinformation om TVSDK 3.13 för iOS
description: Versionsinformation för TVSDK 3.13 för iOS beskriver vad som är nytt eller ändrat, vilka problem som har åtgärdats och kända samt enhetsproblemen i TVSDK iOS 3.13.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '7575'
ht-degree: 0%

---

# Versionsinformation om TVSDK 3.13 för iOS {#tvsdk-for-ios-release-notes}

Versionsinformation för TVSDK 3.12 för iOS beskriver vad som är nytt eller ändrat, vilka problem som har åtgärdats och kända samt enhetsproblemen i TVSDK iOS 3.12.

## System- och programvarukrav {#system-software-requirements}

Innan du laddar ned iOS 3.12 bör du kontrollera att maskinvaru-, operativsystem- och programversionerna uppfyller följande krav:

Operativsystem: iOS 8.0 eller senare.

## iOS TVSDK 3.13

I versionen finns stöd för DEMUXED HLS/CMAF-annonser (pre-roll, midroll och postroll) för LIVE-, VOD- och FER-strömmar.

Korrigeringar av kundrapporterade problem finns på [Lösta problem](#resolved-issues). Information om begränsningar finns i [kända problem och begränsningar](#known-issues-and-limitations).

### Nya funktioner och korrigeringar i tidigare versioner {#whats-new-previous}

**iOS TVSDK 3.12**

Korrigerade ett problem där direktuppspelningen misslyckades efter 15 minuters uppspelning.

**iOS TVSDK 3.11**

Åtgärdade kundproblem där `isFallbackOnInvalidCreativeEnabled` och metod `customParams` gör att programmet kraschar.

**iOS TVSDK 3.10**

* Ett problem där TVSDK-spelaren inte utlöstes har åtgärdats `PTMediaPlayerStatusError` meddelande när nätverket inte är tillgängligt.

**iOS TVSDK 3.9**

* Ett problem har korrigerats där VTT-undertexter inte kan spelas upp vilket medför att appen låses.

* iOS TVSDK 3.9 innehöll det uppdaterade personaliseringscertifikatet.

**Programfix iOS TVSDK 3.8.0.83**

Snabbfixen hade det uppdaterade transportcertifikatet för personalisering.

**iOS TVSDK 3.8**

iOS 13-kompatibilitet och hantering av iOS 13 `UIWebView` API-borttagning.

**iOS TVSDK 3.7**

Snabbkorrigering för ett scenario där uppspelningen stoppades när många annonsmatchningsbegäranden gjordes samtidigt.

**iOS TVSDK 3.6**

**Korrigeringar i klassen av egenskapen wideXML`PTNetworkAdInfo`**

The `vastXML` egenskapen angavs inte korrekt och returnerade ett nollvärde.

**iOS TVSDK 3.5**

**Aktivera bakgrundsljud**

*Konfigurera appen så att ljudet fortsätter att spelas upp när den placeras i bakgrunden.*

För att aktivera den här funktionen måste vi ange det nya API:t `audioPlaybackInBackground` läggs till i `PTMediaPlayer` klassen. När det här API:t är aktiverat kan ditt program spela upp bakgrundsljud.

**iOS TVSDK 3.4.0.19 (programfix)**

Den här versionen innehåller en korrigering för programkrascher som inträffar i ett ad failover-scenario.

**iOS TVSDK 3.4**

**Timeout för annonsupplösning**

* Med TVSDK 3.4 kan man nu ange timeoutvärdet för den övergripande annonsupplösningen och för nedladdningar av manifest. Om vissa annonser inte löses inom en viss tidsgräns spelar TVSDK upp de återstående annonserna.

* `PTAdMetadata: adRequestTimeout` API har tagits bort och tas bort. Standardvärdet är 35 sekunder.

* Två nya alternativa API:er har lagts till i `PTAdMetadataClass: adResolutionTimeout`  - timeout för allmänna annonsupplösningsanrop adManifestTimeout - timeout för hämtningar av annonsmanifest.

**Intäktsoptimering**

Aktiverade TVSDK för att identifiera problemområden som rör arbetsflöden för annonsinfogning och rapportera till analysens slutpunkt.

**Version 3.3**

TVSDK 3.3 följer nu iOS 11 SDK. Alla föråldrade API:er har ersatts med lämpliga alternativ.

**Version 3.2**

**Stöd för ytterligare loggning (fas 2)**

Stöd för felmeddelanden har lagts till om:

* HLS-versionen av annonsen använder högre nivå än innehåll.

* Variant som endast är för ljud är exkluderad.

* VAST/VMAP-begäran misslyckades.

**Version 3.1**

* **Ytterligare loggningsstöd**
Stöd för beskrivande meddelanden har lagts till om det uppstår fel vid annonsuppspelning.

* **Tillagd [!DNL Fairplay] Stöd för krypterad CMAF-ström**
  [!DNL Fairplay] Nu stöds krypterade CMAF-strömmar med AVC-kodekuppspelning.

**Version 3.0.1**

Inga nya funktioner eller förbättringar i den här versionen.

**Version 3.0**

* TVSDK 3.0 stöder HEVC-strömmar.

* Just In Time - Matcha annonser närmare annonsmarkörer.

Tillagd `enableDelayAdLoading` egenskapen för den booleska typen på appnivå för att aktivera JIT. If `enableDelayAdLoading` NEJ, det kommer att `setadMetadata.delayAdLoading`till True (egenskapen i PTAdMetadata-gränssnittet).

När den här egenskapen är aktiverad löser TVSDK alla annonsbrytningar före positionen baserat på det toleransvärde som har definierats. Som standard `delayAdTolerance` är inställt på fem sekunder.

**Version 1.4.45**

För att uppfylla Xcode10 har TVSDK flyttat från `libstdc++` till `libc++`, och därför är den version som minst stöds iOS 7. Tidigare var det iOS 6.

**Version 1.4.44**

Inga nya funktioner eller förbättringar i den här versionen.

**Version 1.4.43**

* TV-liknande upplevelse av att kunna vara med mitt i en annons utan att aktivera spårning av delar av annonser.\
  Exempel: Användaren går med i mitten (vid 40 sekunder) av en 90-sekunders annonsbrytning som består av tre 30-sekunders annonser. Detta är tio sekunder in i den andra annansen i pausen.

   * Den andra annonsen spelas upp för den återstående längden (20 sek) följt av den tredje annonsen.
   * Annonsspårare för delvis uppspelade annonser (andra annonsen) aktiveras inte. Spåraren för endast den tredje annonsen aktiveras.

* Tillagd `enableVodPreroll` egenskapen för Boolean-typen i PTAdMetadata-gränssnittet. Egenskapen kan användas för att aktivera förrullning i en VoD-ström. If `enableVodPreroll` är NO, PSDK spelar inte upp pre-roll. Detta påverkar dock inte mellantullarna. Standardvärdet för `enableVodPreroll` är JA.
* `closedCaptionDisplayEnabled` API för `PTMediaPlayer` gränssnittet är markerat som borttaget från och med iOS v1.4.43. Bestämma om undertexter är tillgängliga för en viss `PTMediaPlayerItem`, granska `subtitlesOptions` egenskap för `PTMediaPlayerMediaItem`.

**Version 1.4.42**

Inga nya funktioner har lagts till i den här versionen. En lista över åtgärdade problem finns i [Lösta problem](#resolved-issues).

**Version 1.4.41**

API-ändringar:

* **isSecure**: Ett nytt API har introducerats ärSäkert för att förhindra att spelaren spelar in och utlöser ett fel. Standardvärdet är true.

* **allowExternalRecording**: Ett nytt API introduceras för att ge möjlighet till airplay-spegling för ett säkert innehåll. Airplay-spegling behandlas därför som inspelning `allowExternalRecording` värdet måste anges till `True`, för att tillåta airplay-spegling eller inställd på `False` för att stoppa airplay-speglingen för säkert innehåll. Som standard `value` är sant.

**Version 1.4.40**

Inga nya funktioner.

**Version 1.4.39**

* iOS TVSDK är certifierat med VHL 2.0.1 och med VHL 2.0.1 med Nielsen.

* iOS TVSDK uppdateras för att göra CRS-förfrågningar från den nya Akamai-värden `primetime-a.akamaihd.net`.

* Den nya värdnamnskonfigurationen ger leverans av CRS-resurser via både HTTP och HTTPS (SSL) i större skala.

**Version 1.4.36**

Integrera och certifiera VHL 2.0 i iOS TVSDK: Minska barriären i `VideoHeartbeatsLibrary` implementering genom att minska komplexiteten i API:erna.

**Version 1.4.34**

**Nätverksannonsinformation**

TVSDK API:er ger nu ytterligare information om VAST-svar från tredje part. Ad ID, Ad System och VAST Ad Extensions finns i `PTNetworkAdInfo` klass tillgänglig via  `networkAdInfo`  på en annonsresurs. Den här informationen kan användas för integrering med andra annonseringsplattformar som **Moat Analytics**.

**Version 1.4.31**

* **Faktureringsmått** För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.

  Varje gång TVSDK genererar en direktuppspelningshändelse börjar spelaren att skicka HTTP-meddelanden regelbundet till Adobe faktureringssystem. Perioden, som kallas fakturerbar varaktighet, kan vara en annan för VOD av standardtyp, VOD av proffskvalitet (aktiverad annonsering i mellanrullar) och direktinnehåll. Standardlängden för varje innehållstyp är 30 minuter, men ditt kontrakt med Adobe avgör de faktiska värdena.

* **Stöd för flera CDN-annonser** TVSDK har nu stöd för Multi-CDN för CRS-annonser. Genom att ange FTP-information för CRS-annonser kan du ange andra CDN-platser än det Adobe-ägda standardnätverket för CDN, till exempel [!DNL Akamai].

**Version 1.4.29**

I `PTSDKConfig` -klassen, `forceHTTPS` API har lagts till.

The `PTSDKConfig` klassen innehåller metoder för att framtvinga SSL på begäranden som görs till Adobe Primetime annonsbeslutsservrar, DRM- och Video Analytics-servrar. Mer information finns i `forceHTTPS` och `isForcingHTTPS` metoder i den här klassen. Om ett manifest läses in via HTTPS, bevarar TVSDK innehållsanvändningen för HTTPS och respekterar denna användning när relativa URL:er läses in från det manifestet.

>[!NOTE]
>
>Begäranden till tredjepartsdomäner som annonsspårning av pixlar, innehålls- och annonsadresser och liknande förfrågningar ändras inte, och det är innehållsleverantörernas och annonsservrarnas ansvar att tillhandahålla URL:er som stöds via HTTPS.

**Version 1.4.18**

Primetime iOS TVSDK har nu stöd för JavaScript-kreatörer som använder VPAID 2.0 för en interaktiv annonsupplevelse i strömmen. Mer information om VPAID 2.0 finns i Stöd för VPAID-annonser.

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
>Nielsen-modulen har tagits bort från TVSDK-bygget och TVSDK kommer snart att uppdateras med en ny Nielsen-integreringsmodul.

**Ad Fallback, Daisy chaining in ad ad selection logic (Zendesk #3103)**

För VAST-annonser (kreatörer) med återgångsregeln aktiverad hanterar TVSDK en annons med en ogiltig MIME-typ som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet. Mer information finns i Lägga till reserv för VAST- och VMAP-annonser.

**Version 1.4.9**

**Svart signalering med alternativ innehållsersättning**

Som en del av TVSDK-uppdateringen från 1.4 stöder nu Adobe också att man går in i och tillbaka från regionala strömavbrott mot linjärt innehåll. TVSDK kan nu bearbeta två manifestfiler parallellt, i huvudversion och alternativt, för att övervaka utpressningssignaler även när alternativ programmering visas i stället för den ursprungliga programmeringen.

**Version 1.4.8**

**Video Heartbeats Library (VHL) uppdaterad till version 1.5**

* Möjlighet att skicka metadata med videostart eller video-/annons-/kapitelstart som kontextdata.

* Mindre nätverkstrafik - antalet pulsslag är i genomsnitt mindre och mindre.

**Version 1.4.7**

* **Individuellt stöd**

Stöd för lokala installationer av Adobe Individualization Server för att anpassa klientens individualiseringsbegäran och gå till en annan slutpunkt.

* **Upplösningsbaserat utdataskydd**

DRM-profiler kan nu ange den högsta tillåtna upplösningen, beroende på enhetens utdataskyddsfunktioner. Till exempel: _Om HDCP är tillgängligt tillåter du att innehåll med en upplösning på upp till 1080p spelas upp, och om HDCP inte är tillgängligt tillåter du att innehåll med en upplösning på upp till 480p spelas upp._

**Version 1.4.4**

* **Video Heartbeats Library (VHL) update to version 1.4.1.1**

   * Lagt till möjlighet att paketera olika analysanvändningsfall, från andra SDK:er eller spelare, med Adobe Analytics Video Essentials.
   * Annonsuppföljning har optimerats genom att `trackAdBreakStart` och `trackAdBreakComplete` metoder. Annonsbrytningen följer av `trackAdStart` och `trackAdComplete` metodanrop.
   * The `playhead` -egenskapen behövs inte längre när annonser spåras.
   * Stöd för Experience Cloud ID-tjänsten har lagts till.

* **Integration med Nielsen SDK**

TVSDK har nu stöd för att skicka mTVR- och MDPR ID3-beacons till Nielsen SDK utan någon anpassad integrering. Ladda ned 3.1.2.19 Nielsen iOS App SDK och följ instruktionerna här i iOS Programmers Guide för att komma igång.

**Version 1.4.0**

* **Svart signalering med alternativ innehållsersättning**

Som en del av uppdateringen 1.4 TVSDK stöder nu även TVSDK att börja med och gå tillbaka från regionala strömavbrott mot linjärt innehåll. TVSDK kan nu bearbeta två manifestfiler parallellt, i huvudversion och alternativt, för att övervaka utpressningssignaler även när alternativ programmering visas i stället för den ursprungliga programmeringen.

* **Ta bort/ersätt C3-annonser**

Nu krävs inget ytterligare förberedelsearbete för att dynamiskt infoga nya annonser i VOD-resurser (video-on-demand) som kommer från C3-fönstret. TVSDK erbjuder nu ett API för att ta bort anpassade innehållsområden och dynamiskt infoga nya annonser. Den här kraftfulla nya funktionen är också användbar i fall där live/linjärt innehåll möts under sändning och omedelbart tas ned för användning som on demand-innehåll utan att man behöver rensa materialet.

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

**iOS TVSDK 3.13**

* (ZD 42085) - Problem med uppspelning i CMAF-strömmar.

* (ZD-43215) - Krasch när spelaren stängs medan en annons pågår.

* (ZD 43210) - iOS HLS-uppspelningen slutar fungera när WebVTT-underrubriken är aktiverad.

**iOS TVSDK 3.12**

* Direktuppspelningen misslyckas efter 15 minuters uppspelning när TVSDK används för iOS 3.10.

### Lösta problem i tidigare versioner {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998) - `isFallbackOnInvalidCreativeEnabled` gör att programmet kraschar.

* (ZD#41289) - `NSInvalidArgumentException` observeras med metoden `customParams` vilket leder till att programmet kraschar.

**iOS TVSDK 3.10**

(ZD#40943) - TVSDK-spelaren fungerar inte `PTMediaPlayerStatusError` meddelande när nätverket inte är tillgängligt.

**iOS TVSDK 3.9**

(ZD#40272) - iOS TVSDK kan inte spela upp VTT-undertexter med 101001-fel och leder till att appen låses.

**iOS TVSDK 3.8**

* (ZD#40087) - iOS kraschar med spelarfel för VOD-innehåll som har upphört att gälla.

* (ZD#40083) - Annonser före rullning fungerar inte för djurbesättningar med `OpportunityGenerator` och spelaren ger fel.

* (ZD#39828) - `CurrentItem` egenskapen saknar nullability-anteckning, vilket gör att spelaren kraschar när spelarstatusen i meddelandet är `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961) - Innehållet kan inte spelas upp i PiP-fönstret (Picture-in-Picture) när ett innehåll har spelats upp, när flera innehåll har konfigurerats för att spelas upp i PiP.

**iOS TVSDK 3.6**

Inga nya problem i den här versionen.

**iOS TVSDK 3.5**

Inga nya problem i den här versionen.

**Version 3.3**

(ZD#37820) - En lista över tillåtna för anpassad rubrik HS-ID, HS-SSAI-TAG har lagts till.

**Version 3.2**

* **Biljett nr 36588** - Spelarkrasch inträffar när STOP-metoden för MediaPlayer anropas.

Korrigerad intermittent krasch som observerades när STOP-metoden anropades för några strömmar med undertexter.

* **Biljett nr 37080** - Dubblettbegäranden för manifestanrop.
Åtgärdade dubblettbegäranden som gjorts för manifest-URL:er under uppspelning. TVSDK gör nu ett anrop per manifest.

* **Biljett nr 37** - CRS-normaliseringsregel misslyckas med matchningstypen eq Åtgärdat ett fall där spelaren kraschade när den påträffades med den senaste normaliseringsregeluppsättningen för värdnamn med matchningstypen &quot;eq&quot;.

**Version 3.1**

**Biljett nr 36313** - Intermittenta oförutsägbara resultat under linjär annonsuppspelning med fasta intermittenta uppspelningar under linjära annonsuppspelningar i liveströmmen.

**Version 3.0.1**

**Biljett36948** - CRS - Sorteringsordningen för tillgångsval överensstämmer inte med iOS 12 Tillgången som väljs för CRS är inte alltid den variant av högsta kvalitet som returneras i ett VAST- eller VMAP-svar.

**Version 3.0**

* **Biljett35311** - Spelarstatus PAUSAS inte under ett avbrutet telefonsamtal Tillagd avbrottshanterare för att hindra spelaren från att avbryta. Vid avbrott ändras spelarstatusen till PAUSED och uppspelningen återupptas när du klickar på uppspelningsknappen.

* **Biljett36685** - Live-resurser - Tidsmatchningsfel med spelarens tidsförlopp och SCTE-markörens tid Korrekt tid beräknas för SCTE-markörerna som ligger före direktpunkten.

* **Biljett36492** - `currentTime` och `localTime` uppdateras inte vid sökning till en ny position under pausad status Spelarens aktuella tid kan nu ställas in på noll om spelaren är i pausat läge. Tidigare var den aktuella tiden inställd på noll endast i uppspelningsläge.

**Version 1.4.45**

* **Biljett36294** - iOS TVSDK fungerar inte med Xcode 10 Åtgärdade kompileringsproblemen med TVSDK i XCode 10. På grund av kraven för XCode 10 kräver appar som bygger på TVSDK för iOS 1.4.45 och framåt ett lägsta distributionsmål som iOS 7.0

* **Biljett36321** - Störningar observerade i sökbart intervall mellan `PTMediaPlayer` och `AVPlayer` instans i _Spelar_ tillstånd.

* **Biljett36493** - `libstdc++` support för iOS 12 Åtgärdade kompileringsproblemen med TVSDK i iOS 12. Appar som bygger på TVSDK för iOS 1.4.45 eller senare kräver ett lägsta distributionsmål som iOS 7.0

**Version 1.4.44**

* **Biljett34683** - Förloppstiden för annonsuppspelning är negativ

Ytterligare kontroller har lagts in för att hantera fallet när det finns en avvikelse mellan den varaktighet som rapporteras av annonsservern och det faktiska annonsinnehållet.

* **Biljett34801** - `currentTime` och `localTime` uppdaterades inte vid sökning till en ny position under pausad status Spelarens aktuella tid kan nu anges till noll om spelaren är i pausat läge. Tidigare var den aktuella tiden inställd på noll endast i uppspelningsläge.

* **Biljett35037** - Spela upp pauser med felaktig URL när du återgår från signalbaserad annonsinfogning.
Förbättrad korrigering för stängda utgåvor nr 34385 i version 1.4.42. Tillagd isAvbruten kod för kontroll och undantagshantering för att göra åtgärdskön mer robust.

**Version 1.4.43**

* (ZD#32990) - iOS: Innehåll spelas upp i stället för annonser på vissa referenspunkter. `selectedMediaOptionInMediaSelectionGroup` API som ingick i AVPlayerItem-gränssnittet har nu flyttats under `AVMediaSelection` i iOS 11. Problemet löstes med det nya API:t.

* (ZD#33683) TVSDK har tagits bort `==` -suffix från metadatasträngarna. Problemet har åtgärdats i tolkningslogiken.

* (ZD#33905) - iOS TVSDK anropar manifestfilerna med två användaragenter. Problemet med användaragenten har åtgärdats i första m3u8-anropet (fall av ny installation). M3u8 har samma användaragenter för alla samtal nu.

* (ZD#34293) - Förrullningar som infogats i LINEAR-strömmar spelas inte upp korrekt på iOS11. Problemet är åtgärdat för pre-roll-annonser.

* (ZD#34684) - När principen för att hoppa över annonser tillämpas visas bildrutor för förrullning i några sekunder. Ett nytt API, `enableVodPreroll` har introducerats för att inaktivera uppspelning före uppspelning i videouppspelning. Standardvärdet för denna API är _Ja_. API:t gör att det inte går att sammanfoga annonsinnehåll i huvudinnehållet.

* (ZD#34765) - Efter anrop `stop()`, har få transportströmssegment fortfarande hämtats. Förbättrade `Stop()` API för att undvika hämtning av de extra segmenten.

* (ZD#34865) - Förrollningsannonser för [!DNL Livestream] trunkeras på iOS. Relaterat till iOS11 och en extra kontroll för att bekräfta om strömmen är pre-roll eller main-content åtgärdar detta problem.

* (ZD#35093) - Korrigerade ett redundansscenario där uppspelningen inte växlar till säkerhetskopieringsströmmen om den primära varianten av strömmen misslyckas vid start (returnerar 404).

**1.4.42 (1.4.42.118)**

* (ZD#34385) - Uppspelningen stoppas med en felaktig URL vid återgång från signalbaserad annonsinfogning.

  Öka det maximala antalet samtidiga för `CustomAVAssetLoaderOperations`så att manifestläsningarna kan fortsätta att köras.

* (ZD#34373) - Slutanvändare kan inte direktuppspela till HDMI-anslutna enheter när direktuppspelningsinspelning inte tillåts.

* (ZD#32678) - TVSDK samlar inte in rätt annons-ID på iOS.

  Annons-ID för den slutliga annonseringen hämtas nu i VHL-pingar om det finns VAST-/VMAP-omdirigeringar.

* (ZD#33904) - TVSDK har inte registrerats för AVFoundation-meddelanden `AVAudioSessionMediaServicesWereLostNotification` och `AVAudioSessionMediaServicesWereResetNotification`.

  `PTMediaServicesWereLostNotification` och `PTMediaServicesWereResetNotification` kan nu registreras i spelarappen för att få meddelanden när medietjänsterna återställs eller förloras.

* (ZD#33815) - Kunderna kan inte uppdatera sina CRS-regler för prioritering och normalisering utan att behöva uppdatera appen.

  Lagt till `getCRSRulesJsonURL` och `setCRSRulesJsonURL` API:er till iOS TVSDK.

**Version 1.4.41 (1.4.41.76)**

* (ZD #34464) - Issues building Reference App with TVSDK Version 1.4.41

  Från och med den här versionen krävs Xcode 9 för kompilering av TVSDK för iOS.
* (ZD #29456) - Airplay startar i pausat läge

  Åtgärdade pausproblemet som uppstod när videon pausades när airplay startades.
* (ZD #30371) - Starttiden för AdBreak ändras när vi infogar mer än två annonser i linjär ström

  Korrigerade felet vid uppspelning av innehåll på Apple TV, vilket förhindrar uppspelning helt
* (ZD #32146)- Nej `PTMediaPlayerStatusError` tas emot för HLS Live-innehåll när iOS 11 dev beta blockeras

  Nej `PTMediaPlayerStatusError` tas emot för HLS Live- och VOD-innehåll om blockering med Charles (Drop connection and 403).

* (ZD #29242) - Airplay-videouppspelning misslyckas med annonser aktiverade.

  När annonser är aktiverade och AirPlay är aktiverat när du börjar spela upp en video, startar aldrig videouppspelningen och inget fel visas.

* (ZD#33341) - `DRMInterface.h` utlösare bygger varningar i Xcode 9.

  Korrigerade två blockprototyper i `DRMInterface.h` som saknade ordet void i sina parameterlistor.

* (ZD#31979) - Kompilerar/körs inte när det är iOS 10 eller senare för iPhone 7/iPhone7+.

  Korrigerad kompilering av IB-dokument för tidigare versioner än iOS 7 stöds inte längre.

* (ZD#32920) - Tom skärm i en annonsbrytning och ingen annonsbrytning slutförs.

  När en annonsbrytning visar annonsförekomster och när en annonsförekomst är klar visas en tom skärm.

* (ZD#32509) - Inaktivera iOS 11 skärminspelning Inaktivera skärminspelning i iOS 11.

* (ZD#33179) - Intermittent händelsefel i iOS11.

  Åtgärdade händelsefelet i iOS 11.

**Version 1.4.40** 1.4.40.72

* (ZD #32465) - Spelaren kan inte hantera sammanfogade spellistor.

  Utlysning `finishLoadingWithError`(med: Fel) för AV-basen för att prova alternativa strömmar/utlösa failover.

* (ZD #31951) - TVSDK-fel under licensroteringar.

  Korrigerade licensrotationsproblemet.
* (ZD #31951) - Tom skärm i en annonsbrytning och ingen annonsbrytning slutförs.

  Ett problem där Facebook VPAID-annonser ofta returnerade flera CDATA-block i ett enda `<AdParameters>` VAST-nod.
* (ZD #33336) - iOS TVSDK - Ad pods not be fill, trots att tillräckligt många annonser returnerades av Freewheel.

  Skapade en överordnad-underordnad relation mellan sekvensannons och reservannons och sortering baserat på överordnad sekvens och index.

**Version 1.4.39** 1.4.39.43

* (ZD #32178) - iOS TVSDK-versionen är felaktig.

  TVSDK-versionen i loggfilerna var 1.0.211. Den är fast för att få rätt version.

* (ZD #32199) - Lazy Ad loading - Video visas inte för innehållet.

  Den lokala Adbreak-tidslinjen som inte initierades tidigare uppdateras nu innan den används.

* (ZD #27528) - Video, ljud eller båda fryser 1-45 sekunder efter att en resurs börjar spelas upp, om det sekundära ljudet är inställt på icke-standard i iOS 1.2.

  Förbered och informera ljudspår i tillståndet Ready.

* (ZD #30411) - Du kan få oväntade resultat, till exempel inget ljud eller felaktigt ljud, om du väljer ett sekundärt Sap-språk.

  Förbered och informera ljudspår i tillståndet Ready.

* (ZD #32199) - Lazy Ad loading - Video visas inte för innehållet.

  Den lokala Adbreak-tidslinjen som inte initierades tidigare uppdateras nu innan den används.

* (ZD #27528) - Video, ljud eller båda fryser 1-45 sekunder efter att en resurs börjar spelas upp, om det sekundära ljudet är inställt på icke-standard i iOS 1.2.

  Förbered och informera ljudspår i tillståndet Ready.

* (ZD #30411) - Du kan få oväntade resultat, till exempel inget ljud eller felaktigt ljud, om du väljer ett sekundärt Sap-språk.

  Förbered och informera ljudspår i tillståndet Ready.

**Version 1.4.38** 1.4.38.860

* (ZD #29281) - iOS: Lägg till AdSystem och Creative Id i CRS-begäranden

Användning av kreativt ID och AdSystem i CRS-begäran baserat på CRS-normaliseringsregler

* (ZD #29176) - krasch den `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

Krasch på grund av tom AdBreak hanteras nu.

* (ZD #30125) - Programmatiska annonser fungerar inte i iOS

Stöd för programmatiska annonser i iOS.

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

Problemet är åtgärdat. iOS TVSDK tar fram en `exception(AUDNetworkAdInfo::initWithAdId)` och inte hantera det. Undantaget beror på ett tomt ID.

* (ZD #29281) - Lägg till AdSystem och Creative ID i CRS-begäranden.

Inkludera AdSystem och CreativeId som nya parametrar i förfrågningarna 1401 och 1403 (alla andra parametrar är desamma).

**Version 1.4.35** 1.4.35.830

* (ZD #27830) - Måste programmässigt avgöra skillnaden mellan undertexter och undertexter i iOS.

TVSDK visar nu de två typerna som kan användas för att filtrera ut den bildtexttyp som krävs.

* (ZD #29160) - EXT-X-CUE-OUT ad ad cues delas inte in korrekt i TVSDK iOS.

EXT-X-CUE-OUT-mikrofon spelas nu upp.

* (ZD #29100) - Programmet kraschar när användaren drar till slutet av en film.

Flera krascher relaterade till synkronisering har korrigerats.

* (ZD #28785), (ZD #27712) och (ZD #25076) - iOS-appen kraschar under de stora liveeventen.

Flera krascher relaterade till synkronisering har korrigerats.

**Version 1.4.34** (1.4.34.815 för iOS 6.0+)

* (ZD #28481) - FER-avbrott på grund av att fel tangent läggs till i slutet av en annonsbrytning för dessa FER-strömmar

För en FER-ström infogas nyckeln före annonsbrytningen efter slutet av annonsbrytningen. Problemet löstes genom att *senast synlig nyckel* efter annonsbrytningen.

**Version 1.4.33** (1.4.33.803 för iOS 6.0+)

* (ZD# 21701) Aktivera CRS för underkonton

Aktiveras genom att den ursprungliga kreativa URL:en för 1401 CRS-begäran skickas i stället för den normaliserade URL:en, enligt kravet för CRS back end.

* (ZD# 26218) - `PSDKResources.bundle` inläsningsproblem

Problemet löstes genom att resursinläsningen uppdaterades för att se från alla tillgängliga paket.

* (ZD# 27460) Midroll first Ad call - POST to `cdn.auditude.com` returnerar 403.

Det nya CDN-kontot kan inte hantera en CDN-begäran för POST. Problemet löstes genom att koden uppdaterades för att `cdn.auditude.com` och begär att få vara GET istället för POST.

**Version 1.4.32** (1.4.32.792 för iOS 6.0+)

* (ZD# 27132) Stöd för decimalvärden för VMAP-annonsbrytningar.

När innehåll inte segmenterades längs de definierade annonsbrytningarna orsakade heltal oväntade annonsplaceringar. Problemet löstes genom att decimalvärdena inte konverterades till heltal.

* (ZD# 27189) AES-innehåll med taggen EXT-X-DISCONTINUITY-SEQUENCE spelas inte upp korrekt.

Problemet löstes genom att taggen placerades i början av spellistan.

**Version 1.4.31** (1.4.31.785 för iOS 6.0+)

* (ZD# 24528) Implementera TVSDK-användningsstatistik för fakturering

Mer information finns i [Faktureringsmått].

* (ZD# 24642) Stöd för bild-i-bild för TVSDK

Bild-i-bild-funktionen som ibland inte fungerade som den ska har åtgärdats.

* (ZD# 25246) Felaktiga brytningssignaler

Problemet löstes genom att sammanföra diskontinuitetstaggar i olika variantmanifest.

* (ZD# 26218) Programbyggprocessen blir komplicerad när du försöker inkludera `PSDKLibrary.framework` i klientens programramverk

Problemet löstes genom att paketera `PSDKLibrary.framework` på begäran.

* (ZD# 26364) Multi-CDN-stöd för CRS-annonser

Mer information finns i Multiple CDN-stöd för CRS-annonsleverans.

* (ZD# 27028) Fördröjning vid uppspelning av vissa strömmar i iOS 10.

Problemet löstes genom en tillfällig lösning för strömmar som inte har ett M3U8-tillägg.

**Version 1.4.30** (1.4.30.754 för iOS 6.0+)

Följande problem löstes för TVSDK i den här versionen:

* (ZD# 24180) Lägg till en anpassad rubrik i tillåtelselista.

En ny anpassad rubrik har lagts till i TVSDK-tillåtelselista.

* (ZD# 25016) Redundansström väljs slumpmässigt när ABR-kontrollparametrar anges

Problemet löstes genom att ABR-strömmarna bibehölls i den ordning som ABR-inställningarna medföljer `initialBitrate` inställning för en ström som innehåller URL:er för växling vid fel. På så sätt undviker du att spela upp failover-strömmarna i stället för primärt.

* (ZD# 25076) Krasch den `PTAuditudeAdResolver loadComplete`

Problemet där en krasch inträffade vid snabb start/stopp av flera PTMediaPlayer-instanser med annonser har åtgärdats.

* (ZD# 25960) Inga fler prenumerationstaggar utlöser utsändningar av meddelanden om metadataändringar

Problemet där en prenumerationstagg inte meddelas när den visas innan det första segmentet i manifestet har korrigerats.

* (ZD# 26084) PSDK som ger 106000.101000.-11833 Det gick inte att hitta något fel vid övergång från den senaste annonsbrytningen till underhållningsinnehåll

När den sista starttiden för en annonsbrytning från VMAP infaller innan den totala längden är slutförd, infogas i vissa fall inte nyckeln förrän efter slutet av den sista annonsbrytningen. Problemet har åtgärdats.

* VHL (Video Heartbeat Library) har uppdaterats till version 1.5.9 för att lösa följande problem:

* (ZD #22351) VHL - Analys: Varaktighet för livevideoresurs

Problemet löstes genom att  `assetDuration`  API till `PTVideoAnalyticsTrackingMetadata` för att uppdatera resursens varaktighet för direktuppspelning/linjär direktuppspelning och tillhandahålla en logik för att kontrollera direktuppspelningen.

* (ZD# 22675) VHL - Analys: Uppdatera varaktigheten för livevideoresurs

Problemet är detsamma som ZD #22351.

* (ZD #25908) VHL - Analys: Adobe pulsslagshändelsekrasch

Problemet löstes genom att implementeringen uppdaterades för att använda den senaste versionen av VHL för iOS version 1.5.9 för att förbättra stabilitet och prestanda.

* (ZD #25956) VHL - Analys: Krasch vid upprepade uppspelningar av videor

Problemet är detsamma som ZD #25908.

**Version 1.4.29** 1.4.29.743

* (ZD# 23901) Annonser från tredje part spelas inte upp

Problemet löstes genom att URL-strukturen för CRS v3 flyttades så att zon-ID inkluderades i den ompaketerade URL:en.

* (ZD #25183) Problem med DRM-uppspelning på tvOS och iOS

Problemet löstes genom stöd för flera nyckeltaggar som behövs för stöd av flera DRM.

* (ZD# 25334) TVSDK kan inte spela upp ett delat cDVR-innehåll

Problemet löstes genom att TVSDK inte kunde konvertera tomma strängar till absoluta URL:er.

* (ZD# 25347) Ange anpassad HTTP-rubrik för AVURLAsset

Stöd för anpassade rubriker på segmentbegäranden via `PTNetworkConfiguration` har lagts till.

**Version 1.4.28** 1.4.28.722

* (ZD #24549) Flera annonseringsanrop

Problemet löstes genom att tidslinjehanteraren uppdaterades för att lyssna efter meddelanden på ett specifikt objekt när flera spelare skapades.

* (ZD #24758) `PTManifestLogger` stöder inte iOS 8

Problemet löstes genom att logger-verktygsbiblioteket uppdaterades till distributionsmålet version 7.0.

* (ZD #24775) Fördröjd ström på grund av annonser

Problemet löstes genom korrekt beräkning av varaktigheten i händelsespellistor.

* (ZD #24799) Vissa avsnitt spelas inte upp i iOS APP

Problemet löstes genom att den lokala webbservern användes för undertexter när WebVTT-filerna är geografiskt begränsade.

**Version 1.4.27** (1.4.27.711) för iOS 6.0+

* (ZD #24089) - Optimeringar för annonsupplösning på långa DVR-strömmar

Problemet löstes genom att flera optimeringar lades till för att minska den tid som krävs för att bearbeta DVR-fönstret i live/linjära strömmar.

* (ZD #21554) - felfyrar i TVSDK inte aktiverade för `application-type = video/mp4`

Problemet löstes genom att spelaren aktiverade att pinga rätt URL för felspårning i ogiltiga resursformat.

* (ZD #24424) - Textkrasch `EXC_BAD_ACCESS KERN_INVALID_ADDRESS` har sitt ursprung inifrån `PSDKLib` för iOS på nyare maskinvaruenheter.

Kraschen som inträffade på grund av en avallokerad mediespelarinstans, när uppspelningen växlas snabbt mellan olika strömmar, har åtgärdats.

* (ZD #24575) - Krasch i TVSDK på 32-bitarsenheter när `enableDebugLog=true`

Problemet med loggformatet som orsakade kraschen på 32-bitarsenheter när loggning är aktiverat har åtgärdats.

**Version 1.4.26** (1.4.26.702) för iOS 6.0+

* (ZD# 20213) - TVSDK FW måste vara dynamiskt/modulariserat för XCode7

Åtgärdat genom att uppdatera biblioteken med modulstöd

**Version 1.4.25** (1.4.25.684) för iOS 6.0+

* (ZD #19629) - Live Video Pauses when Entering Airplay to ATV 4

Problemet löstes genom att en vänteperiod läggs till efter att gamla objekt har tagits bort, men innan nya objekt läggs till i `AVQueuePlayer`. Utan vänteperioden skickas meddelanden till fel objekt.

* (ZD #19856) - Inga undertexter visas när de är aktiverade som standard

Problemen i webbspellistan, som fick undertexterna att inte visas korrekt, har åtgärdats.

* (ZD #21590) - Videoprestanda och -spårning i Senaste origin-byggen

Problemet med den saknade videolängden i `VideoAnalytics` har åtgärdats.

* (ZD #20202) - iOS-appen kraschar om du ställer in anpassade undertextningsformat

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

Problemet löstes genom att logiken för att ta bort spelarvyn uppdaterades om en VPAID-annons inte kan spelas upp.

* (ZD #20101) - Anpassad kapitelimplementering startar kapitelstarthändelse under annonsuppspelning

Problemet löstes genom en uppdatering `VideoAnalyticsTracker` för att korrekt identifiera inledande/fullständiga kapitelövergångar vid övergång mellan kapitelgränser och icke-kapitelgränser.

* (ZD #20784) - Analys: Triggering content complete for live video transitions

Problemet löstes genom att en logik lades till för att manuellt aktivera slutförandet av innehåll under en videospårningssession.

Följande bibliotek uppdaterades:

* AdobeMobile-bibliotek till 4.10.0
* VHL-bibliotek till 1.5.6
* Biblioteket VHL-Nielsen till 1.6.7
* (ZD #21855) - Undertexter spelas inte upp efter mittrullen

I det här problemet orsakade duplicerade diskontinuitetstaggar att undertexter inte skulle visas efter mittrullen. Problemet löstes genom att ta bort de diskontinuitetstaggar som finns bredvid varandra.

* (ZD #21994) - Sträng utanför tillåtet intervall `PTHLSUtils`

Den troligaste orsaken till kraschen är när en EXT-X-KEY har en URL som omges av citattecken.

* ZD #22074) - `AUDVAST` Krasch som inträffar en gång i minuten på iOS

I version 1.4.23 har kraschen som orsakades av osäkra tecken i en VAST-omdirigerings-URL åtgärdats. TVSDK fortsatte dock att hoppa över dessa annonser.

Problemet löstes genom hantering av osäkra tecken och genom att annonserna kunde spelas upp.

* (ZD #22694) - `PTMediaPlayer`.  Vyn är dold av spelaren

Problemet löstes genom att logiken för att ta bort spelarvyn uppdaterades om en VPAID-annons inte kan spelas upp.

**Version 1.4.23** (1.4.23.641) för iOS 6.0+

* (ZD #18016) - Inget svar från Primetime SDK med dåligt nätverkstillstånd

Problemet löstes genom att felmeddelanden förbättrades när ett allvarligt fel från `AVFoundation` inträffar och så att programmet kan hantera omstarten efter felet.

* (ZD #20580) - krasch i `PTSplicerManager`

Problemet löstes genom att ge ytterligare skydd mot samtidighetsproblem som orsakar kraschen.

* (ZD #21782) - iOS Error Code 10100

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

Problemet där vissa 302 omdirigerade strömmar inte spelades upp har åtgärdats.

* (ZD #19629) - Live Video Pauses when Entering Airplay to ATV 4

Problemet löstes genom att man lade till en tillfällig lösning för direktuppspelning av video när airplay är aktiverat för Apple TV 4-enheter. Problemet verkar vara en utgåva av Apple TV 4.

* (ZD #21119) - TVSDK stoppas efter annonsuppspelning

Stöd har lagts till för AES-krypterade strömmar med sekvens IV när annonsinfogning används.

* (ZD #21125) - Återgå från live/linjär och brytning tidigt

Stöd har lagts till för att gå tillbaka från en annonsbrytning tidigt innan annonsbrytningen spelas upp tills den är klar. Tidig retur anges med en anpassad manifesttagg.

* (ZD #21224) - Airplay-stöd för tokeniserade strömmar från Akamai

API:er har lagts till i `PTNetworkConfiguration` klass för att lägga till cookies som URL-parametrar i segment för vissa tokeniserade Akamai-strömmar.

* (ZD #21287) - Överflödig logg

Ett problem med vissa loggsatser som visas som standard i xcode-konsolen har korrigerats även när loggning är inaktiverad.

* (ZD #21446) - Ad Break-händelser aktiveras ibland inte av TVSDK

I EVENT-strömmar aktiveras annonsbrytningar inte korrekt i den tidigare versionen. Den här versionen åtgärdar det här problemet.

**Version 1.4.21** (1.4.21.605) för iOS 6.0+

* (ZD #20749) - Fallback hoppar över VAST-svar som inte är tomma, extra URL:er för annonsspårning

Ett problem med dubblettping på reservannonser har lösts.

**Version 1.4.20** (1.4.20.590) för iOS 6.0+

* (ZD #18639) - TVSDK använder för mycket processorkapacitet/resurser på en lång het-inspelningsresurs

Överdriven processoranvändning/resursanvändning har fastställts på två nivåer. Först genom att låta tidsuppdateringsfunktionen köras på en global kö i stället för på huvudtråden och genom att optimera CPU-användningen för att analysera manifestet med den tidigare bearbetade och cachelagrade m3u8.

* (ZD #19349) - Annonser före rullning hoppas över när nätverksanslutningen stryps.

Problemet löstes genom att en timeout-händelse (requestTimeout) angavs för programmet och `adMetadata.adRequestTimeout` API för att åsidosätta standardtidsgränsen på 10 sekunder.

* (ZD #19446) - Meddelande saknas i liveströmmar

Problemet löstes genom att programmet fick abonnera på `EXT-X-PROGRAM-DATE-TIME` på liveströmmar.

* (ZD #19459) - Krasch vid förberedelse av alternativt ljud med `PTMediaPlayerItem` `prepareAudioOptionsWithAVMediaSelectionOptions`
* (ZD #19460) - Krasch - `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

Problemet är detsamma som Zendesk #19459.

* (ZD #19574) - TVSDK returnerar inte M3U8-svarsdata för DRM- eller icke-DRM-innehåll

I den första inläsningen av manifestfilen i `PTMediaPlayerItem.prepareToPlay`Om det inte gick att läsa in manifestet rapporterar TVSDK inte brödtexten för felsvaret på programmet.

Problemet löstes genom att TVSDK fick rapportera felsvaret som ett fel till programmet.

* (ZD #19615) - Återställningslogiken fungerar inte

I den aktuella implementeringen hoppades reservannonser över och packades inte om såvida inte dessa annonser är i m3u8-format. Problemet löstes genom att även stödet för ompaketering av reservannonser lades till.

* (ZD #19770) - TVSDK kan inte spela upp skyddat AES-innehåll med 302-omdirigering

Omdirigeringsproblemet har åtgärdats eftersom omdirigerings-URL:en har rensats av `cleanConnectionData` innan den kunde användas för att analysera manifestet.

* (ZD #19856) - Undertexter visas inte för vissa bithastigheter när de aktiveras som standard

Problemet löstes genom att felet från iOS hanterades för de segment i strömmarna där undertexterna inte visas.

* (ZD #19868) - TVSDK kraschar när en ogiltig kreatör handlas

Kraschen i TVSDK som felaktigt avallokerade en instans av den stora parsern har åtgärdats.

* (ZD #20180) - VPAID-annonser hoppas över ibland

JavaScript Mime-typen inkluderades inte alltid eller ansågs vara en giltig MIME-typ. Problemet löstes genom att JavaScript inkluderades som en giltig MIME-typ.

* (ZD #20749) - Fallback hoppar över VAST-svar som inte är tomma, extra URL:er för annonsspårning

Problemet med att en del kreatörer inte packas om har åtgärdats.

**Version 1.4.19** (1.4.19.563) för iOS 6.0+

* ZD #18639) - TVSDK använder mycket processorkapacitet/resurser på en lång het inspelningsresurs

Problemet löstes genom att DRM m3u8-spellistan optimerades så att den skrivs om till cachelagrade bitar av spellistan som tidigare har skrivits om. Detta är mest relevant när du spelar upp live m3u8-strömmar för vilka m3u8 laddas ned efter varje segmentnedladdning.

* (ZD#18956) - `player.drmManager` är noll när brytpunkten anges i iOS Demo Player

Problemet löstes genom att uppdatera `PTMediaPlayer.drmManager` API-implementering för att hämta DRMManager från DRM-ramverket.

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

* (Zendesk #3304) - VAST 3.0 `[ERRORCODE]` makrot fylls inte i

Problemet där [!DNL Auditude] SDK kan inte skicka ett ping när spårnings-URL:en har blanksteg i början.

* (Zendesk #17294) - krasch [!DNL SecKeyRawSign]

En eventuell krasch när kundens kod använder nyckelkedjan har lösts.

* (Zendesk #18008) - Stöd för cookies för iOS8+ för tokeniserade strömmar

Akamai-tokeniserade strömmar kräver att cookies skickas vid segmentbegäranden, vilket inte var möjligt i iOS 7 och tidigare. Från och med iOS 8 har Apple lagt till ett API som tillåter att cookies skickas för segmentbegäranden. Detta stöd finns nu i TVSDK. Stöd har också lagts till för att skicka en användaragent, om tillgängligt.

* (Zendesk #18166) - TVSDK 1.4.15 ger hundratals varningar vid kompilering med `DWARF` med `dSYM` filalternativ

Alla varningar har åtgärdats.

**Anteckning**: tvOS-kompatibla bibliotek har lagts till för TVSDK.

**Version 1.4.16** 1.4.16.1454

* Zendesk #3875 - Tab S kraschar vid uppspelning

Återställa beroendet av OKHTTP på [!DNL Auditude] för CRS eftersom TVSDK nu använder `httpurlconnection` i stället för att rulla. Problemet löstes genom att undantagen rensades innan ett nytt JNI-anrop gjordes.

* (Zendesk #4487) - Spårning av innehållets linjära kanal

Problemet löstes genom ominitiering av spåraren för pulsslag i videon under en linjär direktuppspelningssession.

* (Zendesk #17919) - Android - innehållssökning orsakar hjärtslagsfel

Problemet var att lösa pulsslag i ett feltillstånd när det finns en sökning i ett kapitel

* (Zendesk #18053) - Program som använder TVSDK kraschar på Marshmallow

TVSDK kraschade i operativsystemet Android™ M när TVSDK-biblioteket använder neonkod som gör YUV `->` RGB färgkonvertering. Problemet löstes genom att funktionerna som orsakar problemet uppdaterades med en icke-neon version av `code`.

* (Zendesk #18072) - Android M - Application Crash

Den här kraschen inträffar vid anrop `MediaCodecList` och `MediaCodecInfo` API:er vid kontroll av om profilen och nivån stöds. Adobe söker Google support för ytterligare information. Problemet löstes genom att en tillfällig tillfällig tillfällig lösning skapades genom att all codec-information lästes in i förväg för att undvika att anropa dessa API:er endast när kodekinformation behövs.

* (Zendesk #18074) - Arabiska undertexter som inte fungerar på Nexus med Android™ 6.0

Problemet löstes genom stöd för teckensnittskartan i Android™ CTS.

**Version 1.4.15** (1.4.15.512) för iOS 6.0+

**Anteckning**: Nielsen-modulen har tagits bort från TVSDK-bygget, men TVSDK kommer snart att uppdateras med en ny Nielsen-integreringsmodul.

* (ZD #2228) - Ett fel returnerades när manifestet hämtades som inte är tillgängligt i `MediaPlayerNotification`

Lagt till metadata för att visa innehåll när meddelandet `M3U8_PARSER_ERROR` inträffar.

* (ZD #4437) - kraschar i Adobe Primetime SDK

Korrigerade en rapporterad krasch vid förberedelse av undertexter/alternativt ljud.

* (ZD #4487) - Spårning av innehållets linjära kanal

Tillåts ominitiering av spårningsfunktionen för pulsslag under en linjär direktuppspelningssession.

**Version 1.4.14** (1.4.14.498) för iOS 6.0+

* (ZD #17260) - krasch den `playlistManagerForURL`

Korrigerade en intermittent krasch på grund av samtidighetsproblem.

**Version 1.4.13** (iOS 6.0+)

* (ZD #3304) - VAST 3.0 `[ERRORCODE]` makrot fylls inte i

   * Felkod 400 visas om intern annonsering har dålig kreativitet.
   * `[ERRORCODE]` makrot är URL-kodat.

* (ZD #3865) Integrering av pulsslag med IMA-annonser

Korrigerade ett fel där videolängden rapporterades felaktigt.

* TSDK-demospelaren för iOS 9 har uppdaterats

Om du vill ha stöd för iOS 9 måste du konfigurera undantagen i Application Transportation Security. För demonstrationen är ATS helt inaktiverat.

**Version 1.4.12** (1.4.12.464) för iOS 6.0+

* (ZD #4521) CRS Testing Client Side och SSAI

Korrigerat felaktig omvänd MD5 i 3P-URL.

**Version 1.4.12** (1.4.12.463) för iOS 6.0+

* (ZD #2751) CSAI och CRS / Förbättra: Hantera dynamiska element i vissa URL:er för mediefiler.

Uppdaterad Creative Repackaging Service för att hantera annonser med dynamiska kreativa URL:er.

* (ZD #3654) Minnesläcka i PSDK-version efter 1.3.4.166

Minnesläcka som åtgärdats `drmFramework` med regelbunden uppspelning på iOS 8.2-enheter

* (ZD #3988) Förhandsgranskning hoppas över vid återsökning efter första uppspelningen

Korrigerade ett fel så att annonsprinciper kunde inaktiveras korrekt.

* (ZD #4017) Begär att iOS API ska tvinga annonsuppspelning på bakåtriktad sökning

Löst med fix för ZD #4279

* (ZD #4279) HLS TVSDK ad insertion -302 redirect issue on iOS and Desktop

Ett fel har korrigerats när en annonsresurs använde en relativ omdirigerings-URL

**Version 1.4.9** (1.4.9.427) för iOS 6.0+

* (ZD #3075) Internet Reachability Issue - iOS

Meddelande har lagts till för att identifiera när uppspelningen har avstannat.

* (ZD #3193) Begäran om ett API för profiländring i TVSDK

Uppdaterat `PTPlaybackInformation` för att visa den uppdaterade angivna bithastigheten. Uppdaterat `BITRATE_CHANGE` som är mer tidstillförlitlig och korrekt i förhållande till de M3U8-rapporterade bithastigheterna.

* (ZD #3324) Primetime-annonser rapporterar problem när inga annonser finns i VMAP

Stöd för pingning av tomma URL:er för annonsspårning, TVSDK verifierar nu start av annonsbrytning och kompletta pingar för tomma annonsbrytningar.

**Version 1.4.8** 1.4.8.402)

* (ZD #3158) IOS 7 kraschar vid repriser av fullständiga händelser

**Version 1.4.7** 1.4.7.382

* (ZD #2197) Spårning och fel. Det gick inte att läsa in manifestet för det tillagda meddelandet för resursen.
* (ZD #2894) Spelaren gör fyra manifestbegäranden på den översta nivån under uppspelning.
* (ZD #2992) [!DNL Auditude] Rapportera konstiga varaktigheter och identifierare.

**Version 1.4.6** 1.4.6.325

* (ZD #2197) Spårning och fel. Tillagda meddelanden för resursen kunde inte läsa in manifestet

**Version 1.4.5** 1.4.5.283

* (ZD #2141) Analysimplementering för [!DNL TreeHouse] app, tillagd `AdobeAnalyticsPlugin.a` bibliotek för att skapa paket.
* Video Heartbeats Library update to 1.4.1.2
* (PTPALY-4226) (relaterat till ZD #2423) Om du utför DRM-återställning kan programdokumentdata tas bort.

**Version 1.4.4** 1.4.4.242

* Video Heartbeats Library (VHL) update to 1.4.1.

* (ZD #2435) TV SDK-dokumentation om uppdateringar av analysbehov

**Version 1.4.2** (1.4.2.210: iOS 6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` returnerar tomt
* (ZD #2109) Primetime PSDK 1.4.1.125 fungerar inte med Xcode 5.1.1
* (ZD #2137) Krasch i PSDK på iOS när DRM-metadata inte kan läsas in

**Version 1.4.1** 1.4.1.125

* (ZD #1107) [!DNL CocoaLumberjack] duplicera symboler
* (ZD #1644) Ändra iOS-användaragent för målgruppsanpassning och rapportering
* (ZD #1850) Cocoa Lumberjack-filer som ingår i iOS SDK
* (ZD#1908) Anpassade taggar ignoreras av PSDK om det finns fler än 1

**Version 1.4.0** 1.4.0.32

* Zendesk #1024 - Funktion för att ta bort annonser från strömmen via manifest

## Enhetscertifiering och support {#device-certification-and-support}

>[!NOTE]
>
>Följande funktioner är **not** stöds i TVSDK:
>
>* Långsam rörelse, oavsett plattform eller version.
>* Livetrick.

**Version 1.4.43**

* TVSDK 1.4.43 är certifierat för iOS 11.

**Version 1.4.29**

* TVSDK 1.4.29 har certifierats för iOS 10.

**Version 1.4.28**

* TVSDK 1.4.28 har certifierats för iOS 10 Beta 7.
* DRM-stöd som tvingar HTTPS genom att lägga till  `forceHTTPS`  och `isForcingHTTPS` API.
* VHL-bibliotek har uppdaterats till 1.5.8, Adobe Mobile-bibliotek till 4.8.4 och loggningsverktygsbiblioteket till version 7.0-distributionsmålet.

**Version 1.4.19**

Den här versionen av TVSDK har certifierats med FairPlay-stöd för iOS och tvOS.

**Version 1.4.17**

* tvOS

  Den här versionen av TVSDK har stöd för tvOS och har certifierats för okrypterade HLS-strömmar.

  **Anteckning**: Kom ihåg följande riktlinjer för kompilering:

   * Stödet för tvOs i TVSDK är begränsat till DRM-krypterade strömmar som inte är Adobe. Du måste ta bort referensen till `drmNativeInterface.framework` i dina inställningar för tvOS-bygge. AES-krypterade strömmar stöds fortfarande.
   * Apple kräver att alla Apple TV-program är bitkodsaktiverade, så du måste aktivera den här flaggan i projektinställningarna.

## Kända fel och begränsningar {#known-issues-and-limitations}

* På grund av borttagning av klassen iOS UIWebView i iOS TVSDK 3.6 och framåt:
   * VPAID-annonser spelas inte upp som förväntat i iPad 13.
   * Kompletta annonser fungerar inte som förväntat.

* I iOS TVSDK sammanfogas alla annonser i innehållsmanifestet. Annonsbeteenden implementeras genom att söka baserat på innehållets och annonssegmentens varaktighet. Så om segmentens varaktighet inte är korrekt kanske sökningen inte alltid avslutas vid den exakta bildrutan i början eller slutet av annonsbrytningen. Även om varaktigheten är för bildrutan finns det en tolerans som plattformen själv tillämpar på sökning och det kan finnas några ramar, annonser eller innehåll som visas. Detta är en begränsning av plattformen och hur annonsinfogning fungerar med TVSDK på iOS.
* Beslutet att hoppa över inträffar för seek-händelsen i det här fallet. Men eftersom längden på annonssegmentet i manifestet inte representerar annonsens faktiska längd korrekt, är sökningen inte korrekt. Därför visas några bildrutor med annonser när annonspolicyer tillämpas.
* Det kan hända att licensrotationsvideo inte spelas upp på iOS 11 och att den spelas upp som den ska på iOS 9.x och iOS 10.x.
* Om uppspelningen är aktiv över AirPlay hoppas VPAID-annonser över i VPAID 2.0-stödet.
* The `drmNativeInterface.framework` länkar inte korrekt när minimimålet är iOS7 (eller senare).
Tillfällig lösning: Ange explicit `libstdc++.6.dylib` bibliotek enligt följande: Gå till **[!UICONTROL Target]** > **[!UICONTROL Build Phases]** > **[!UICONTROL Link Binary With Libraries]** och lägga till `libstdc++.6.dylib`.
* Det gick inte att infoga post-roll-API:t för ersättning.
* Om du söker efter en annonsbrytning (utan att komma ut ur den) utfärdas en dubblett av meddelanden om annonsstart och annonsbrytningar
* Inställning `currentTimeUpdateInterval` har ingen effekt.
Obs! I vissa iOS-versioner läser operativsystemet inte in resurserna i `PSDKLibrary.framework` automatiskt. Det är viktigt att kopiera `PSDKResources.bundle` till programmets paketresurser: Gå till **Skapa faser** och kopiera paketresurser.
* Referensappen kan inte byggas med Xcode 8 eller tidigare versioner. iOS TVSDK version 1.4.41 och senare, använd Xcode 9 för att kompilera.
* VPAID-annonser följer inte `delayAdLoadingTolerance` värde.
* 24077 - För visst HLS-innehåll med undertexter kraschar spelaren på _Stoppa_ eller _Återställ_ -metod.
* Detaljerade felmeddelanden är inte tillgängliga om bara in Time Ad Resolution är aktiverat.
* Felmeddelanden loggas enligt annonsupplösningstiden och inte enligt annonssekvensen.
* HEVC-stödet har följande begränsningar i den här versionen
   * DRM stöds inte
   * CC (CEA 608/708) stöds inte eftersom det inte stöds i CMAF.
   * 4K-stöd finns ännu inte.
   * ID3-taggar stöds inte eftersom det inte stöds i CMAF.
   * Omultiplicerade Live HEVC-strömmar har inte verifierats.
   * Stöd för HEVC-annonser har inte verifierats.
* När JIT är aktiverat och toleransen är inställd på 10 sekunder visas inget VAST-anrop för den första fabriken och brytningen om det finns VMAP > VAST-omdirigeringsannonser.
* För att tidsgränsen för annonsupplösning ska fungera korrekt förväntar sig spelaren en sammanslagen spellista inom 20 sekunder varje gång spellistan uppdateras under direktuppspelning. Om den inte får en sammansatt spelningslista inom det angivna intervallet genereras ett internt fel och spelaren stoppas.

## Användbara resurser {#helpful-resources}

* [TVSDK 3.4 for iOS Programmer&#39;s Guide](/help/programming/tvsdk-3x-ios-prog/ios-3x-introduction/ios-3x-overview/ios-3x-overview.md)
* [TVSDK API-referens för iOS 3.4](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* Se den fullständiga hjälpdokumentationen på [Adobe Primetime Läs mer &amp; Support](https://experienceleague.adobe.com/docs/primetime.html) sida.
