---
title: Versionsinformation om TVSDK 1.4 för Android
seo-title: Versionsinformation om TVSDK 1.4 för Android
description: Versionsinformation om TVSDK 1.4 för Android beskriver vad som är nytt eller ändrat, de lösta och kända problemen samt enhetsproblemen i TVSDK Android 1.4.
seo-description: Versionsinformation om TVSDK 1.4 för Android beskriver vad som är nytt eller ändrat, de lösta och kända problemen samt enhetsproblemen i TVSDK Android 1.4.
uuid: 8bd8ee42-7a1b-4c14-aad9-22804743e505
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: f1ebc1a8-185a-493a-9c00-a6102dffb128
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '7830'
ht-degree: 0%

---


# Versionsinformation för TVSDK 1.4 för Android {#tvsdk-for-android-release-notes}

Versionsinformation om TVSDK 1.4 för Android beskriver vad som är nytt eller ändrat, de lösta och kända problemen samt enhetsproblemen i TVSDK Android 1.4.

## Nya funktioner {#new-features}

**Version 1.4.43**

**Säker annonsinläsning över HTTPS**

Adobe Primetime erbjuder ett alternativ för att begära första anrop till en primetime-annonsserver och CRS via HTTPS.

**alwaysUseAudioOutputLatency(booleskt val) i klassen MediaPlayer**

När den här parametern är inställd använder du fördröjningen för ljudutgångar i tidsstämpelberäkningen för ljud.

Den accepterar booleska parametrar val. Om värdet är `True` använder klienten fördröjningen för ljudutdata i tidsstämpelberäkningen för ljud.

**Version 1.4.42**

**Delvis annonsinfogning:**
TV-liknande upplevelse av att gå med mitt i en annons utan att aktivera spårning för den delvis bevakade annonsen.
Exempel: Användaren går med i mitten (vid 40 sekunder) av en 90-sekunders annonsbrytning som består av tre 30-sekunders annonser. Detta är tio sekunder in i den andra annansen i pausen.
* Den andra annonsen spelas upp för den återstående längden (20 sek) följt av den tredje annonsen.
* Ad trackers for the part ad ad ad ad (second ad) are not fire. Spåraren för endast den tredje annonsen aktiveras.

**Version 1.4.41**

Inga nya funktioner.

**Version 1.4.40**

Inga nya funktioner.

>[!NOTE]
>
>Du behöver inte ändra API:t om du använder en tidigare version än 1.4.39.

**Version 1.4.39**

* TVSDK är certifierat med VHL 2.0.1 och med VHL 2.0.1 med Nielsen.
* Android TVSDK har uppdaterats för att göra CRS-begäranden från den nya Akamai-värden `primetime-a.akamaihd.net`.
* Den nya värdnamnskonfigurationen ger leverans av CRS-resurser via både HTTP och HTTPS (SSL) i större skala.
* TVSDK har stöd för Android Oreo.
* En ny funktion läggs till i klassen `AdClientFactory` som har stöd för registrering av flera Säljprojektionsidentifierare:

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   Detta bör returnera en array med PlacementOpportunityDetector. Nu kan du registrera flera projektidentifierare. För till exempel funktionen för tidig annons krävdes två Detectors för säljprojekt - en för annonsinfogning och en för tidig avslutning av annonsen. Du behöver bara implementera den här nya funktionen om du har implementerat en egen AdvertisingFactory (och inte använder DefaultAdvertisingfactory). För att få fram det befintliga beteendet måste du skapa en enda Opportunity Detector, som i funktionen createOpportunityDetector(), som placeras i en array och returneras:

   ```
   public class MyAdvertisingFactory extends AdvertisingFactory {  
   …  
   @Override  
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {  
   List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();  
   opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));  
   return opportunityDetectors;  
   } }
   ```

>[!NOTE]
>
>Du behöver inte ändra API:t om du använder en tidigare version än 1.4.39.

**Version 1.4.36**

Felkorrigering för Innehållsväxling på Android.

**Version 1.4.35**

* **Nätverksannonsinformation**

   TVSDK API:er ger nu ytterligare information om VAST-svar från tredje part. Ad ID, Ad System och VAST Ad Extensions finns i klassen NetworkAdInfo som är tillgänglig via egenskapen networkAdInfo på en annonsresurs. Den här informationen kan användas för integrering med andra annonseringsplattformar som **Moat Analytics**.

**Version 1.4.31**

**Multi-CDN-stöd för CRS-annonser**
* Som standard lagras alla omkodade resurser på ett CDN som ägs av Adobe på Akamai. Med den senaste versionen kan Adobe Creative Repackaging Service (CRS) överföra de trancoded creatives till flera CDN:er enligt kundens specifikationer.
* Nya API:er läggs till i TVSDK för att göra det möjligt att ange den slutliga kreativa URL:en för CRS när standardwebbadressen inte används. Läs dokumentationen för att lära dig hur du använder dessa nya API:er.

**Version 1.4.18**
Primetime Android TVSDK har nu stöd för VPAID 2.0 Javascript-kreatörer för en interaktiv annonsupplevelse i strömmen. Mer information om VPAID 2.0 finns i [VPAID och support](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**Version 1.4.17**

AC-3 5.1 stöds bara på Amazon FireTV.

**Version 1.4.11**

* **Ad Fallback, Daisy chaining in ad ad selection logic (Zendesk #3103** For VAST ads (creatives) with the fallback rule enabled), behandlar TVSDK en annons med en ogiltig MIME-typ som en tom annons och försöker använda reservannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.

Mer information finns i [Lägg till reservversioner för VAST- och VMAP-annonser](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **Video Heartbeats Library (VHL) uppdaterad till version 1.5**
   * Möjlighet att skicka metadata med videostart och/eller video-/annons-/kapitelstart som kontextdata
   * Mindre nätverkstrafik - antalet pulsslag är i genomsnitt mindre och mindre

**Version 1.4.7**

* **Individuellt** stöd för personalisering på platsStöd för lokala installationer av Adobe Individualization Server för att anpassa klientens individualiseringsbegäran till en annan slutpunkt.

**Version 1.4.6**

* **Sample AES-kryptering (kräver Flash Player version 17.0.0.134)**Sample-based AES-kryptering stöds nu.

**Version 1.4.2**

* **Video Heartbeats Library (VHL) update to version 1.4.0.1**

   * Lagt till möjlighet att paketera olika analysanvändningsfall, från andra SDK:er eller spelare, med Adobe Analytics Video Essentials.
   * Annonsspårning har optimerats genom att metoderna trackAdBreakStart och trackAdBreakComplete har tagits bort. Annonsbrytningen härleds från metodanropen trackAdStart och trackAdComplete.
   * Spelhuvudegenskapen behövs inte längre när annonser spåras.

* **Nielsen SDK** IntegrationTVSDK har nu stöd för att skicka användarspårningsinformation till Nielsen SDK utan någon anpassad integrering.

**Version 1.4.0**

* **Svartsignalering med alternativ innehållsersättningSom en del av TVSDK-uppdateringen (1.4) har TVSDK nu också stöd för att börja och återgå från regionala utfall mot linjärt innehåll.** TVSDK kan nu bearbeta två manifestfiler parallellt, i huvudversion och alternativt, för att övervaka utpressningssignaler även när alternativ programmering visas i stället för den ursprungliga programmeringen.

* **Ta bort/ersätt C3** AdsNu behövs inget ytterligare förberedelsearbete för att dynamiskt infoga nya annonser i VOD-resurser (video-on-demand) som kommer ut från C3-fönstret. TVSDK erbjuder nu ett API för att ta bort anpassade innehållsområden och dynamiskt infoga nya annonser. Den här kraftfulla nya funktionen är också användbar i fall där live/linjärt innehåll möts under sändning och omedelbart tas ned för användning som on demand-innehåll utan att man behöver ägna tid åt att&quot;rensa&quot; materialet.

* Gränssnittet PlaybackEventListener har en ny metod som kallas onReplaceMediaPlayerItem, som du kan använda för att avlyssna en ny händelse, `ITEM_REPLACED`. Den här händelsen skickas när en MediaPlayerItem-instans ersätts i MediaPlayer. Klientprogrammet som implementerar denna PlaybackEventListener måste implementera eller åsidosätta den här nya metoden.
* AdClientFactory har en ny funktion som har lagts till i klassen för att registrera flera olika typer av affärsmöjlighetsidentifierare:

   ```
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem item);
   
   For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for  early  exit from  `ad`.
   
   To override this new function create a single Opportunity Detector, and put into an array and return:
   
   @Override
   
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {
   
   List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();
   
   opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));
   
   return opportunityDetectors;
   }
   
   }
   ```

## TVSDK-ändringar för 1.4 {#tvsdk-changes}

* Gränssnittet PlaybackEventListener har en ny metod som heter onReplaceMediaPlayerItem, som du kan använda för att avlyssna en ny händelse, ITEM_REPLACED. Den här händelsen skickas när en MediaPlayerItem-instans ersätts i MediaPlayer. Klientprogrammet som implementerar denna PlaybackEventListener måste implementera eller åsidosätta den här nya metoden.

* AdClientFactory har en ny funktion som har lagts till i klassen för att registrera flera olika typer av affärsmöjlighetsidentifierare:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Om du till exempel har en funktion för tidig annons behöver du två detektorer för säljprojekt - en för annonsinfogning och en för tidig avslutning av annonsen.

Om du vill åsidosätta den här nya funktionen skapar du en enda möjlighet att upptäcka och placera i en array och returnera:

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## Enhetscertifiering och stöd i 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Följande funktioner stöds **inte** i TVSDK:
>
>* Långsam rörelse, oavsett plattform eller version.
>* Livetrick.


**Version 1.4.43**

TVSDK 1.4.43 har certifierats med Android-enheter som har Android 6.0.1/ 7.0 och 8.1 (Oreo).

* **Version 1.4.23:**

   * TVSDK 1.4.23 har certifierats för Android-enheter med Android N.

* **Version 1.4.18:**

   * Primetime har certifierats för Amazon Fire TV.
   * VPAID 2.0 stöds bara på enheter med Android 4.0 och senare.

## Lösta problem i 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Alla TVSDK-kunder som använder CRS bör uppgradera till TVSDK 1.4.39 eller senare på iOS och Android. Uppgraderingen ersätter den befintliga appimplementeringen. Efter uppgraderingen söker du efter CRS Creative URL-begäranden i ett proxyverktyg (till exempel Charles) för att kontrollera att versionen i sökvägen återspeglar version 3.1. Till exempel:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Version 1.4.43**

* Biljett nr 27143 - Det går inte att spela upp 5.1-ljudspår på FireTV-enheter

   * TVSDK kan nu spela upp AC3-ljud på FireTV-enheter. Uppspelningen är alltid i stereo.

* Biljett nr 33902 - Säker annonsleverans via HTTPS

   * Adobe Primetime har ett alternativ för att begära att få ett första anrop till en primetime-annonsserver och CRS via https.

* Biljett nr 34493 - Bluetooth-ljudfördröjning

   * `alwaysUseAudioOutputLatency` har lagts till i MediaPlayer-klassen som när den är inställd resulterar i att fördröjning för ljudutdata används vid beräkning av tidsstämpling för ljud.

* Biljett nr 34949 - ny version av VHL (Video Heartbeat library) integrerat.

**Version 1.4.42 (1791)**

* Zendesk #33719: Adaptiv bithastighet för FireTV 4k skalas långsamt. Stöd för ABR för FireTV 4K-enheter har lagts till.
* Zendesk #33338:  resetDRM rensar alla data i programmet.  Hanterade extra fall där undantag i icke-TVSDK-trådar orsakade att TVSDK-åtgärdsköer fylldes.

**Version 1.4.41 (1776)**

* Zendesk #33002 - Companion asset data from TVSDK on Fire TV. Implementerade en ny klass, AdBannerAsset, som returnerar kompletterande data som List &lt;AdBannerAsset> och AdAsset::id är nu en sträng i stället för lång.
* Zendesk #32821 - Android Primetime-spelaren fryser när den påträffar tidsstämpel för presentation (PTS) för WWE. Problemet har åtgärdats i den här versionen.
* Zendesk #33572 - VideoAnalyticsProvider och Start Crash. Problemet har åtgärdats med rätt kombination av VHL+Nielsen joint SDK-versionen av VideoHeartbeat.jar.
* Zendesk #33355 - Fire TV: 15 sekunder tillbaka. Det är inte någon korrigering från TVSDK:s sida och kunden som verifierar detta hos End och Third party.

**Version 1.4.40 (1764)**

* Zendesk #33068 - Amazon läppsynkroniseringsproblem på ny enhet. Problem med läppsynkronisering har åtgärdats i den här versionen.
* Zendesk #32215 - Android TVSDK 1.4.38 Security Issues `[Hotlist]`. Uppdaterat till senaste OpenSSL-1.1.0 och curl-7.5.1.
* Zendesk #32920 - Tom skärm i en annonsbrytning och utan annonsbrytning. Korrigerade ett problem där en VPAID-behållare kunde hamna i ett obefintligt tillstånd och hanterade ett problem där Facebook VPAID-annonser ofta returnerade flera CDATA-block i en enda \&amp;lt;AdParameters\&amp;gt. VAST-nod.

**Version 1.4.39 (1744)**

* Zendesk #28976 - Licensbegäran tar mer än en sekund. DRM-licensbegärandeanrop som använder POST körs, medan Curl lägger till &quot;Expect: 100-continue&quot;. Tog bort rubriken&quot;Expect:&quot; i TVSDK.
* Zendesk #27707 - CSAI-miljöer som inte följer CUE IN-markörer för tidig återgång till innehåll. Stöd för flera olika generatorer.

**Version 1.4.38 (1722)**

* Zendesk #21590 - Video Performance and Tracking in Latest Origin Builds

Integrera och certifiera VHL 2.0 i TVSDK för att minska barriären i implementeringen av VideoHeartbeatsLibrary genom att minska komplexiteten i API:erna.

* Zendesk #29688 - Support för Android O Beta-kunder.

TVSDK-stöd för den nya betaversionen av Android.

**Version 1.4.36 (1713)**

* Zendesk #27392 - Content Skip on Android

Android TVSDK utökade byteintervallet för innehåll som inte är iframe felaktigt med 16 byte för att rymma dekrypteringen. Det krävs en breddning för Iframe-strömmar men inte för icke-iframe-strömmar.

**Version 1.4.34 (1702)**

* Zendesk #27638 - Leak in cURL INet object

Posix cURL INet-objektet lästes in medan det hölls kvar i resurshanteraren och DNS-cachen som användes i cURL-anslutningarna.

Problemet löstes genom att Posix cURL INet-objektet togs bort från INet-dekonstruktorn.

**Version 1.4.33 (1694)**

* **OpenSSL-bibliotek**

OpenSSL-biblioteket har uppdaterats med OpenSSL version 1.0.2j.

* Zendesk #21701 - Skicka den ursprungliga kreativa URL:en för 1401 CRS-begäran i stället för den normaliserade URL:en.
Problemet åtgärdas genom att de ursprungliga kreativa URL:erna skickas.

* Zendesk #25023 - Lång videouppspelning: frysa video, skärmflimmer
Problemet löstes genom att de maximala videoformatdimensionerna för enheter med CenturyLink set-top box angavs.

* Zendesk #27460 - Det nya Akamai-kontot kan inte hantera en POSTS-cdn-begäran.
Koden uppdaterades för att göra `cdn.auditude.com`-annonsbegäran till GET i stället för POST.

* Zendesk #28245 - Uppspelningsläget meddelas inte korrekt när programmet går från bakgrund till förgrund
Problemet löstes genom att uppspelningsläget återställdes korrekt för att spelas upp eller pausas när programmet återgår till förgrunden.

**Version 1.4.32 (1682)**

* Zendesk #25779 - Säkerhetslucka i TVSDK
Android 4.2 och tidigare har en säkerhetslucka när JavaScript är aktiverat i en WebView. Användning av WebView från TVSDK har inaktiverats för enheter som kör OS 4.2 eller senare. Detta inaktiverar användningen av VPAID-annonser i TVSDK på dessa enheter.

* Zendesk #26890 - Issue in SCREEN state (ON/OFF) handling Ref. Player
När AVE (Adobe Video Engine) återupptas från ett SUSPENDED-läge uppdateras inte statusen för DefaultMediaPlayer. Detta resulterar i att DefaultMediaPlayer förblir i läget SUSPENDED även om AVE är i läget PLAYING. Problemet har lösts genom att tillståndet DefaultMediaPlayer har ställts in på PLAYING när en PLAY-status tas emot från AVE, även om den aktuella statusen för DefaultMediaPlayer är SUSPENDED.

**Version 1.4.31 (1675)**

* Zendesk #21974 - Undantag på grund av null-objekt
   * AdIndex ökas sällan när värdet är null. Detta kan bero på felaktiga API-anrop för pre-roll adBreak. Åtgärdade datatyperna för att undvika sådana undantag

* Zendesk #24714 - Inaktivera överflödig loggning
   * TVSDK har uppdaterats för att inaktivera överflödig loggning

* Zendesk #24488 - AV Sync issues on Fire TV
   * Åtgärdat genom att förbättra hanteringen av AV-avkodartrådarna. När in- eller utdatabildrutorna ändras körs avkodartråden som är specifik för ramens innehållstyp.

* Zendesk #26551 - Åtgärda CRS-fel
   * När begäran är HEAD (http head) behöver vi inte läsa innehållet eftersom det är tomt. Det är ok att försöka läsa det, men gamla Android (4.0.x) hänger sig när read() anropas och nya Android returnerar korrekt värde (-1) när read() anropas. Baserat på detta har koden ändrats till att inte läsa innehåll för head

* Zendesk #26696 Null-pekarundantag vid åtkomst till TrickPlayManager
   * Korrigeras genom att kontrollera om TrickPlayManager-objektet inte är null innan det används.

**Version 1.4.30 (1659)**

* Zendesk #22675 Resurslängden uppdateras inte för Live-/Linear-strömmar
Problemet löstes genom att ett nytt API, assetDuration, i PTVideoAnalyticsTrackingMetadata som anger resursens varaktighet för live- och linjära strömmar angavs.

* Zendesk #25853 Minnesläcka i TVSDK vid byte av kanaler
Problemet där en filläsad buffert läses när MediaPlayer återställs eller släpps när en fil hämtas har åtgärdats.

**Version 1.4.29 (1653)**

* Zendesk #21200 - Spelaren återställs inte från pausat läge när appen fanns i bakgrunden
När spelaren pausades efter att strömbrytaren signalerades, tillåter upplösningen spelaren att utföra strömbrytaren när spelaren återställs från pausläget i stället för att återställa till föregående position.

* Zendesk #23412 - Spelaren har en svart låda om du klickar igenom någon annons inom de sista tre sekunderna av annonsbrytningen
Det här problemet är samma problem som Zendesk #21200.

* Zendesk #23616 - Annullering som hoppats över söker för långt i framtiden
Beroende på annonsinfogningstypen (infoga/ersätt) avgör TVSDK om annonsens varaktighet används i beräkningen för att fastställa slutpunkten för annonsbrytningen.

* Zendesk #25078 - TVSDK DRM Memory leak on Android TV STB
Minnesläckan för DRM-adapterobjektet har hittats och korrigerats.

* Zendesk #25067 - Crash in VideoEngineTimeline
Detta beror på att objekt inte rensades korrekt och händelser anropades efter att objekten förstördes. Problemet löstes genom att kontroller lades till för att förhindra null-undantag.

* Zendesk #25352 - Set custom HTTP header
Problemet löstes genom att en ny anpassad rubrik lades till tillåtelselista på TVSDK.

* Zendesk #25617 - Live stream PTS-rollover orsakar avbrott i spelaren och minneskrasch
Problemet löstes genom att en PTS-överrullningshantering lades till i FragmentedHTTPStreamer när en överrullning sker mitt i ett segment.

**Version 1.4.28 (1637)**

* Zendesk #23618 - Annonshändelser som utlöses innan annonspolicyn hörs
Problemet löstes genom att inte aktivera händelserna AD_BREAK_START och AD_START när annonsen hoppas över på grund av adForgitivity. Händelsen AD_BREAK_SKIPPED skickas i stället.

**Version 1.4.27 (1631)**

* Zendesk #23174 - Prestandaproblem vid storleksändring av video
Problemet löstes genom att ett nytt API, MediaPlayerView.setSurfaceFixedSize, som gör att TVSDK kan komma åt SurfaceHolder.setFixedSize() från MediaPlayerView har identifierats.

* Zendesk #24450 - TVSDK gör dubbla annonsförfrågningar
Problemet uppstod när den förflutna tiden konverterades till lång och inte dubbel, och problemet har åtgärdats.

**Version 1.4.26 (1627)**

* Zendesk #21436 - OpenSSL-biblioteksuppdatering till version 1.0.2h Uppdaterat OpenSSL-biblioteket till OpenSSL version 1.0.2h
* Zendesk #23825 - Cookies ingår inte i återanropen Fixed by provide the support for android cookies.

**Version 1.4.25 (1620)**

* Zendesk #22900 - Live Adobe Primetime DRM-strömmen spelas inte upp i Androids referensspelare
Minnesallokeringsproblemet har åtgärdats.
* Zendesk #23176 - Programmet kraschar när det försöker spela upp VPAID-annonser
Kraschen inträffade eftersom programmet inte skapar en anpassad annonsvy för att återge en VPAID-annons. Problemet löstes genom att man ignorerade VPAID-annonserna i annonsserverns svar när det inte finns någon anpassad annonsvy.

* Zendesk #23153 - SampleAES DRM Stream - Playback stalling in the TVSDK Reference Player
Problemet är detsamma som Zendesk #22900.

**Version 1.4.24 (1612)**

* Zendesk #20784 - Analytics: Utlösande av innehåll för live-videoövergångar
Problemet löstes genom att ett API (trackVideoComplete) lades till för att manuellt aktivera slutförandet av innehåll under en live/linjär videospårningssession.

* Zendesk #21977 VideoEngineTimeline kraschar vid placeAdBreak/acceptAd-åtgärd
   * Följande bibliotek uppdaterades:
      * AdobeMobile-bibliotek till version 4.10.0
      * VHL-bibliotek till version 1.5.6
      * VHL-Nielsen-biblioteket till version 1.6.7

Problemet löstes genom att en null-kontroll lades till innan annonser lades till i listan över godkända annonser.

* Zendesk #22313 Bithastigheten för STB:er med Amilogic chipset är inte längre än 1,2 MB
Problemet löstes genom att man i förväg laddade in mediekodekfunktionerna och inaktiverade den sömlösa switchen för enheter med Amilogic-chipset.

* Zendesk #19520 Sample AES HLS-resurs som inte spelas upp i TVSDK-spelare
Problemet löstes genom hantering av flera PMT-beskrivningar för Sample AES-krypterade HLS-strömmar.

**Version 1.4.23 (1602)**

* Zendesk #18852 - Uppdatera logik för kreativt urval baserat på CRS-regler
Problemet löstes genom att en JSON-konfigurationsfil lades till för att ange prioritet för det kreativa urvalet.

* Zendesk #20861 - Android N
Den här versionen har stöd för Android N genom att ta bort möjligheten att direkt använda Android-plattformens systemspecifika bibliotek som inte längre är tillgängliga för program som körs på Android N.

* Zendesk #21018 - Android N krasch
Samma upplösning som ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter kraschar vid ett Invalid_Key-fel
Felet Invalid_Key innehåller ingen beskrivning från AVE, så tolkningen av texten resulterade i NPE. Problemet löstes genom att en null-kontroll för beskrivningen lades till under onError innan beskrivningen tolkades.

* Zendesk #22286 - Det inbyggda biblioteket allokerar minnesläsningsnyckel/fragment vilket orsakar krasch
Den här kraschen som inträffade på Android när ett försök gjordes att läsa in ett manifest med flera nycklar samtidigt har åtgärdats.

**Version 1.4.22 (1581)**

* Zendesk #17236 - Otillförlitlig speltid för HLS-videor med DRM
Tidshoppet med LBA-strömmarna, där starttiden för ljudsegmentet inte matchar starttiden för videosegmentet, har åtgärdats.

* Zendesk #17680 - Videouppspelning är fryst i rutan Selevision Andredo
Videoavkodaren på den här enheten returnerar ibland ett avsevärt tidshopp för utdata när videobildrutan ställs in från utdatabufferten, och den här tidsstämpeln för utdata är fortfarande hög. Problemet löstes genom att en *videoprofil som inte stöds*-fel returnerades som inte tvingar spelaren att försöka med samma profil igen eller välja en annan profil.

* Zendesk #19074 - Video fryser under FFWD- och REW-trick play
Problemet löstes genom att en ny varning, TRICKPLAY_ENDED_DUE_TO_ERROR, lades till för att meddela programmet att trickningen har avslutats och att videon pausades på grund av ett oåterkalleligt fel.

* Zendesk #19574 - TVSDK returnerar inte M3U8-svarsdata för DRM- eller icke-DRM-innehåll
Problemet löstes på följande sätt:

* Zendesk #19986 - Operativsystemets beteende fungerar inte på vissa enheter som Android TV
* Lägger till ett FILE_NOT_FOUND-fel i villkoret.
* När felet kommer från en *fil som inte hittas*-fel avgränsar URL:en och svaret från felbeskrivningen om svaret är tillgängligt.
Logikfelet som introducerades av stödet för NVidia-sköldens OP har åtgärdats. På andra enheter än NVidia-skölden kan du lita på de skyddade skärmsflaggorna även när visningstypen är okänd.

* Zendesk #20549 - Handling of stale playlists. Problemet löstes genom att intervallet mellan uppdateringen av det aktiva manifestet reducerades till hälften av den förväntade segmentlängden om den föregående hämtningen inte tar emot nya segment.

* Zendesk #20742 - Minnesanvändningen verkar fortsätta öka när direktuppspelning av innehåll på FireTV spelas upp. Kraschen orsakas av JNI-objektets referenstabell som har nått gränsen. Problemet löstes genom att referensen till det MediaFormat-objekt som skapades när avkodaren startades om togs bort.

* Zendesk #21125 - Return from live/linear ad ad break early (CSAI). En funktion har lagts till som gör att spelaren kan återgå till huvudinnehållet under en annonsbrytning om spelaren registrerar splice i ad cues genom att använda splice i affärsmöjlighetsdetektorn.

* Zendesk #21334 - TVSDK-annonsbegärans timeout-värde för annonsbegäran från tredje part. En adRequestTimeout-inställning har lagts till i AdvertisingMetadata som aktiverar en global timeout för annonsanropet.

**Version 1.4.21 (1566)**

* Zendesk #17781 - skärmdumpen i ADB fungerar inte längre
Problemet löstes genom att API:t DefaultMediaPlayer.create(Context context, boolean secureSurface) lades till, som tillåter skärmfångst.
Om du vill tillåta skärmdumpar skickar du false för secureSurface.
Viktigt: Vi rekommenderar att du inte aktiverar den här skärmdumpsfunktionen i en produktionsinställning.

* Zendesk #19074 - Video fryser under FFWD- och REW-trick play
Följande problem som uppstod när trickPlay kunde frysa i uppspelningen har lösts:

* Zendesk #19532 - Bildtexten är inte i ordning
   * FHS börjar med trickning, men det första iframe-segmentet hade ingen bildruta i det.
   * När ett iframe-segment hämtas och FHS träffar ett feltillstånd avslutas det från tricks och pausar uppspelningen.
   * Android MediaCodec-implementeringen väntar för alltid på tillgänglighet i indatakö medan den ombads tömma alla in-/utbuffertar.
Problemet löstes genom att ordningen för WebVTT-cues ändrades så att flera överlappande cues visades rulla uppåt.

* Zendesk #19574 - TVSDK returnerar inte M3U8-svarsdata för DRM- eller icke-DRM-innehåll
I den initiala inläsningen av manifestfilen i PTMediaPlayerItem.prepareToPlay rapporterar inte TVSDK brödtexten för felsvaret på programmet om inläsningen misslyckas.
Problemet löstes genom att TVSDK fick rapportera felsvaret som ett fel till programmet.

* Zendesk #19701 - Uppspelningsfrysning med SAP/DisContinuity
Spelaren låser sig när ljud- och videoklippet inte justeras vid avbrott har lösts.

* Fel #PTPLAY-11162 - Uppdateringen av OpenSSL-biblioteket till version 1.0.2f har åtgärdats.

**Version 1.4.20 (1546)**

* Zendesk #17384 - Feature Request: Stöd för ID3-metadata för AAC-uppspelning
Stöd för ID3-taggar i AAC-media finns i TVSDK för Android med början i version 1.4.20.

* Zendesk #18358 - Spelaren fryser på växeln med bithastighet och osynkroniserade avbrott
Problemet löstes genom att man på lämpligt sätt hanterade fall med ABR- stygn.

* Zendesk #19232 - App som använder TVSDK 1.4.18 beter sig underligt i äldre Amazon OS version 4
Problemet löstes genom att den dolda webbvygenereringen i TVSDK-spelarens initieringsprocess togs bort för att undvika konflikter med enheter som inte har stöd för Android-webbvisning.

* Zendesk #19585 - långsam uppspelning när övergången till adaptiv bithastighet sker.
Om den nya profilen vid ABR-växling har en annan samplingsfrekvens för ljud än den aktuella profilen, blir uppspelningen snabb eller långsam. Detta beror på att videopresentatorn inte får något meddelande om att ljudformatet har ändrats.
Problemet löstes genom att kontrollera att meddelandeflaggan är inställd på rätt plats.

* Zendesk #19683 - SAP DAI playback - Inget ljud på några sekunder.
I flera fall i TVSDK:s logik användes RENDITION_TIMEOUT_THRESHOLD som ett godtagbart värdeintervall när tidsstämpeln för två återgivningssegment jämfördes, eftersom tidsstämpeln inte alltid kan matchas med en skillnad på 0 ms. Om mellanrummet ligger inom intervallet RENDITION_TIMEOUT_THRESHOLD, antas det vara en matchning.

RENDITION_TIMEOUT_THRESHOLD angavs till 100 ms, men var inte tillräckligt för vissa strömmar. Problemet löstes genom att RENDITION_TIMEOUT_THRESHOLD ökades till 200 ms.

* Zendesk #19699 - TVSDK växlar inte mellan VTT-undertextspår
Problemet löstes genom att spelardumpen gjordes och manifestet lästes in igen när ett spår ändras och genom att det UTF8-strängkonverteringsproblem som påverkade WebVTT-bildtextens dubbelbyte-namn korrigerades.

* Zendesk #19717 - Visningsproblem med CC-alternativ
Problemet löstes genom att Unicode-strängen hanterades korrekt.

* Zendesk #19910 - TIT2 ID3-taggar kan inte identifieras
Problemet löstes genom att man tillhandahöll mer fullständigt stöd för ID3 v2.4-strängkodning och stöd för ID3 v2.3.

* Zendesk #20135 - TVSDK utlöser flera onComplete-utlösare för VOD-innehåll.
Problemet löstes genom att händelseavlyssnaren post_roll_complete lades till på rätt plats, i stället för vid det fullständiga fallet med statusförändringshändelsen.

**Version 1.4.19 (1521)**

* Zendesk #4180 - TVSDK verkställer inte HDCP.
   * Det här är en partiell korrigering för den här biljetten och åtgärdar bara problemet för NVidia-sköldenheter.
Du måste använda det korrekt implementerade API:t för HDCP-identifiering i Nvidia-skölden för att dynamiskt spåra HDCP-statusen.

* Zendesk #18358 - TVSDK fryser på växeln med bithastighet utan avbrott i synkroniseringen.
   * Problemet löstes genom att en ny varning lades till för att upptäcka avbrott i PTS och genom att PTS-kontrollen tvingades göra om sökningen efter rätt segment för varje ABR-växel.
För att åtgärda frysningen ska anropet till metoden mediaPlayer.setCustomConfiguration innehålla forcePTSCheckForABR som ett argument.

* Zendesk #19038 - No live stream on Asus Zenpad 10.

   Problemet löstes genom att information om mediekodeken lästes in i förväg så att du inte frågar efter funktionen vid körning.

* Följande problem är samma som Zendesk #19038:
   * Zendesk #19483 - TVSDK kraschar på Intel-plattformen.
   * Zendesk #19171 - kraschar på Asus Memo Pad 7 med Android 5.0.

**Version 1.4.18 (1503)**

* Zendesk #3324 - Primetimes annonseringsrapportering spårar inte annonsbrytningar när det inte finns några annonseringsmedier i en VMAP.
När en annonsbrytning är tom fästs inte annonsbrytningens start- och slutspårningshändelserna. Problemet löstes genom att man skickade startpunkter för annonsbrytningar på tomma annonsbrytningar, som VMAP AdBreak, med en giltig AdSource-nod.

* Zendesk #18229 - SetCCViblity(VISIBLE) ignoreras efter anropet till MediaPlayer.reset()
Problemet löstes genom att setCCVisibility(Visibility.INVISIBLE) lades till. till funktionen reset() i klassen MediaPlayer.

* Zendesk #18328 - Utelämnade bildruteproblem på andra generationens Amazon Fire TV-enheter för innehåll med 60 bildrutor/s
Problemet löstes genom att den kodade bildrutefrekvensen användes för beslut om vilotid och med en bättre kodad logik för FPS-förutsägelse.

**Version 1.4.17 (1472)**

* Zendesk #2231 - Ett fel returnerades från hämtning av manifestet som inte är tillgängligt i MediaPlayerNotification
Problemet löstes genom att manifestets svarstext inkluderades när ett tolkningsfel uppstod.

* Zendesk #17703 - VideoEngineView förhindrar inte skärmbilder under videouppspelning
Metoden setSecure har varit tillgänglig sedan API 17, men eftersom API 17 omfattar 4.2, 4.2.1 och 4.2.2 är det inte känt vilken som kommer att generera ett undantag eller om den är enhetsspecifik. Problemet löstes genom att VideoEngineView.setSecure kapslades in i try catch-satsen.

* Zendesk #17919 - Innehållssökning orsakar pulsslagsfel
Ett ogiltigt positioneringsfel för indata uppstod som ett resultat av pulsslagsanropet som genererades när sökningen startades efter förrullningen. Problemet har åtgärdats.

**1.4.16a** (1454a)

* Zendesk #18215 - Vissa AES-strömmar kan inte läsas in.
Problemet löstes genom att storleken på DRM-metadata för profilen kontrollerades innan AES-nyckeln lästes in.

**Version 1.4.16 (1454)**

* Zendesk #3875 - Tab S kraschar vid uppspelning
Återställer beroendet av OKHTTP på Auditude för CRS eftersom TVSDK nu använder httpurlconnection direkt i stället för curl. Problemet löstes genom att undantagen rensades innan något annat JNI-anrop gjordes.

* Zendesk #4487 - Tracking Linear Channel of Content
Problemet löstes genom att man tillät ominitiering av spårningen av pulsslag i videon under en linjär direktuppspelningssession.

* Zendesk #17919 - Android - Innehållssökning orsakar hjärtslagsfel
Problemet när pulsslag är i feltillstånd när det finns en sökning i ett kapitel har lösts.

* Zendesk #18053 - Adobe Primetime kraschar på Marshmallow
TVSDK kraschade i Android M OS när TVSDK-biblioteket använde neonkod som utför YUV-> RGB-färgkonverteringen. Problemet löstes genom att funktionerna som orsakar problemet uppdaterades med hjälp av den icke-neonversion av koden.

* Zendesk #18072 - Android M - Application Crash
När du kontrollerar om profilen och nivån stöds inträffar en krasch när API:erna MediaCodecList och MediaCodecInfo anropas. Problemet löstes genom att man temporärt kunde kringgå problemet genom att läsa in all codec-information i förväg för att undvika att anropa dessa API:er endast när kodekinformation behövs.

* Zendesk #18074 - Arabiska undertexter som inte fungerar på Nexus med Android 6.0
Problemet löstes genom att CTS-teckensnittskartan för Android tillhandahölls.

**Version 1.4.15 uppdatering (1438)**

* Zendesk #17437 - Lång fördröjning av start av VOD-innehåll med vissa AES-strömmar.
För att lösa problemet hämtar du alla AES-nycklar parallellt om det finns flera nycklar i manifestet.

**Version 1.4.15 (1435)**

* Zendesk #4278 - Glitches on Android set top boxes when Adaptive birate changes (ABR).
Korrigeringen var att lägga till stöd för sömlös ABR-växling med den senaste Android-mediekodeken.

* Zendesk #17063 - Anrop av mediaPlayer.reset() orsakar ett fel i återställningen av videomotorn.
Korrigeringen var att inkludera den ursprungliga MediaErrorCode från VideoEngineExceptions när ErrorEvents skickades.

* Zendesk #17130 - En kort men märkbar paus när bithastigheten ändras som visas på FireTV.
(Samma som #4278 ovan) Korrigeringen var att lägga till stöd för sömlös ABR-växling med den senaste Android-mediekodeken.

* Zendesk #17666 - Ytterligare annonsmarkörer, oväntade eller inga annonser när innehållet återupptas.
Korrigeringen var ett problem när VOD-innehåll (PreparateToPlay on video-on-demand) skulle användas. Den initiala sökningen utförs på lokal tid i stället för på virtuell tid.

* Zendesk #17437 - Lång fördröjning av start av VOD-innehåll med vissa AES-strömmar.
Korrigeringen var att ladda ned alla AES-nycklar parallellt när flera nycklar anges i manifestet.

* Zendesk #17851 - Android TV - Black Frame under ABR
Korrigeringen var att ange KEY_MAX_WIDTH och KEY_MAX_HEIGHT för att aktivera adaptiv uppspelning.

**Version 1.4.14 (1415)**

* Zendesk #3875 - Tab S kraschar vid uppspelning.
Ytterligare en åtgärd krävdes för att förhindra kraschen.

* Zendesk #17245 - Fallback på Android TV fungerar inte.
Ett ytterligare problem har korrigerats där uppspelningen hänger sig när reservfunktionen är aktiverad och VMAP-svaret har en tom annonsbrytning.

**Version 1.4.14 (1412)**

* Zendesk #17245 - Fallback på Android TV fungerar inte.
Borttagen en begränsning för inaktivering av kreativ ompackning för reservannonser.

**Version 1.4.13 (1388)**

* Zendesk #3502 - Stöd för klientbaserad HLS-failover under en annonsbrytning
Tillåt växling till huvudmanifestet när fel uppstår i direktprofilen under annonsbrytningsperioden.

* Zendesk #3875 - Tab S kraschar vid uppspelning
Använd ett tredjepartsbibliotek för att lösa konflikten mellan HttpUrlConnection och cURLm.

* Zendesk #4450 - issue setting custom meta data for a single placement in a content resolver
Lägg till en set-metod i inställningarna för säljprojekt.

**Version 1.4.12 (1388)**

* Zendesk #2751 - CSAI and CRS | Förbättra: Hantera dynamiska element i vissa URL-adresser för mediefiler.
Uppdaterad Creative Repackaging Service för att hantera annonser med dynamiska kreativa URL:er.

* Zendesk #3965 - Om du växlar tillbaka till normal uppspelning från trickning kommer uppspelningen att hoppa framåt en bit innan uppspelningen startar.
   * I Fix ingår att TVSDK returnerar tiden innan hastighetsändringen tills alla variabler har uppdaterats, i stället för att försöka beräkna GetStreamTime.
   * Korrigerad krasch vid ändring av trickhastigheten nära strömmens slut.
   * Korrigerad beräkning av aktuell tid under trick play.

* Zendesk #3978 - Trickplay på 8x och 16x fryser ofta.
   * Välj alltid trippelprofilen med den lägsta bithastigheten för att undvika konstant buffring.
   * Öka hoppbildruteintervallet för hög trippelfrekvens.
   * Åtgärda ett problem som gör att bufferten fortsätter att växa efter att mållängden uppnåtts under trick play.

* Zendesk #3992 - Additional Trickplay speed.
TrickPlay har uppdaterats för att acceptera frekvenser över 16x. +/- 32, +/-64 och +/-128 tillåts nu också.

* Zendesk #4007 - Tolka GEOB-objektet som en del av tidslinjemetadata (Android &amp; Web).
Lagt till API:t setByteArray och getByteArray.

* PTPLAY-7301 - Direkt start vid slumpmässig åtkomstpunkt.
Instant On har uppdaterats för att tillåta en startpunkt som inte är noll.

**Version 1.4.11 (1363)**

* Zendesk #2076 - Vanlig slutare vid uppspelning av video på Motorola Xoom med Android 4.0.3
Enheter som lagts till i tillåtelselista för att förhindra att de försöker spela upp innehåll med hög profil.

* Zendesk #2197 - `[Ads]` Spårning och fel
skicka OperationFailedEvent med varningsmeddelande.

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]`-makro fylls inte i
   * felkod 400 visas om annonsen är intern och har dålig kreativitet.
   * `[ERRORCODE]` makrot kommer att vara URL-kodat

**Version 1.4.10 (1354)**

* Zendesk #2941 - Live assets does not have &quot;0&quot; in seekable range
Tidigare fanns det en 3-segmentbuffert när du sökte till början av en Live-ström, men nu är det möjligt att söka till början av en liveström (dvs. början av det första segmentet).

* Zendesk #3169 - Uppdatera referensspelaren med Adobe Analytics-integrering. Referensspelaren har uppdaterats med Adobe Analytics-biblioteket som en exempelimplementering.
* Zendesk #3299 - Oförklarligt trickbeteende
   * Korrigerade ett fel där det kunde ta flera sekunder att återgå till uppspelningsläget efter att tricket stoppats (ibland 25+ sekunder).
   * Korrigerade ett fel där ett anrop av trick spelas upp en andra gång på samma media, vilket kan göra att strömmen fryser vid den aktuella tiden.
* Zendesk #3433 - Android och Flash - Problem med undertexter

GetLine för WebVTT respekterar inte den justerade längden &lt;CR>&lt;LF> för ett paket; den sista bildtexten kan innehålla tecken från tidigare bildtexter.

* PTPLAY-6243 - Förbättra referensspelaren för att hämta felsökningsinformation

Exempelreferensspelarna för Android har förbättrats med ett alternativ för att aktivera felsökningsloggar och skicka resultaten via e-post. Det här alternativet finns under loggmenyn i referensspelaren.

**Version 1.4.9 (1332)**

* Zendesk #2649 - Bufferten är slutförd innan den inledande bufferten är full

Efter en sökning kan videomotorn ange läget PLAYING innan videopresentatorn är klar att spelas upp. Inträffar när buffertläget är högt före sökning. Åtgärda genom att meddela videomotorn att bufferten är låg. Om videomotorn har ett lågt buffertläge ändras läget till BUFFERING i stället för PLAYING när uppspelning anropas. Uppspelningen återupptas när läget ändras till SPELNING.

* Zendesk #2846 - Enhancement request: Gör det möjligt att ange en annan användaragentsträng för anrop från Auditude-biblioteket

Ett nytt API har lagts till för att ställa in användaragenten för annonsrelaterade anrop, audiudeSettings.setUserAgent(&quot;användare/agent&quot;). Om ingen användaragent är inställd används standardinställningen. Detta påverkar bara användaragenten för annonseringsrelaterade anrop. Användaragenten för medieanrop ändras inte, vilket är &quot;Adobe Primetime&quot;+&lt;standardanvändaragent>.

**Version 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Error with local ... Om det inte går att läsa in manifestet i FragmentedHTTPStreamer::ThreadParseManifest() kontrollerar du om URL-domänen är localhost och i så fall ändrar domänen till 127.0.0.1 och återkallar ThreadParseManifest.
* Zendesk #3072 - Automatisk växling till lägre bithastighet. Beräkningen av buffertlängd har ändrats så att noll PTS-nyttolast hoppas över.
* Zendesk #3168 - WebVTT-undertexter som endast visas under de första 10 sekunderna.
* Zendesk #3193 - Request for a Profile change API in TVSDK, PlaybackEventListener.onProfileChanged() has been added.

**Version 1.4.7 (1311)**

* Zendesk #2197 - Tracking and errors. Tillagda meddelanden för resursen kunde inte läsa in manifestet
* Zendesk #2575 - PSDK ignorerar MARK-anpassad annons före video
* Zendesk #2719 - Win Döden med audiouthyrning, fast spårning av fyrar när den omdirigeras till relativ url i audio plugin
* Zendesk #2760 - Taggen DISCONTINUITY ignoreras i TrickPlay-läge
* Zendesk #2805 - Player kraschar vid början av uppspelningen, samma korrigering som Zendesk #2719
* Zendesk #2817 - Android player - Spelaren hänger och stoppar ibland uppspelningen, fast genom att utöka avkodningsbuffertarna från 2,0 till 3,0 sekunder
* Zendesk #2839 - Stöder Adobe Primetime PSDK ARMv8-chipsets?, och har lagt till fix för krasch som hittats i Galaxy S6.
* Zendesk #2885 - Auditude Crashing playback, samma korrigering som Zendesk #2719
* Zendesk #2895 - HLS-fel i realtid efter 10 minuters uppspelning
* Zendesk #2925 - Feedback om Android-dev-bygge (1.4.5), på vissa enheter när paketet köas till indatakön, om PTS är negativt, försätts avkodaren i ett konstigt tillstånd att vi alltid får negativa utdata-PTS för framtida paket. Korrigeringen ställer in PTS-indata på noll om det är negativt för att undvika det här problemet.
* PTPLAY-4645 - Inaktivera stöd för RC4-chiffrering i openssl. Det finns kända explosioner för RC4. Det innebär att om ett försök görs att ansluta till en server som bara stöder RC4, kommer det att misslyckas.

**Version 1.4.6 (1282)**

* Zendesk #2192 - Bithastigheten är inte alltid lägre vid dåliga nätverksförhållanden, som åtgärdas genom att man tar bort snabb switchimplementering.
* Zendesk #2631 - Arabiska undertexter på Android: Text på flera rader visas som brytpunkt, fast genom att justera teckenstorleken för arabiska teckensnitt.
* Zendesk #2844 - Buffring on Note 4 and Fragment download time is not correct.

Problemet löstes genom att man lade till fördröjning mellan nedladdningar av videosegment i bandbreddsberäkning och att beräkningslogiken för nedladdningstid använder en komplett begärandecykeltid.

* Zendesk #2908 - Arabiska undertexter som inte fungerar med Nexust 5, 6 och 7, som åtgärdas genom att ytterligare två grundteckensnitt läggs till för arabiska skript.
* PTPLAY-4627 - uppdatera Nielson appsdk till version 1.2.3.7
* PTPLAY-5084 - Stöd för Överordnad Manifest-uppdatering

**Version 1.4.5 (1248)**

* Zendesk #1757 - Endast ljud som spelas upp eller spelaren kraschar för en videobithastighetsprofil, Nexus 4 och Nexus 7 kraschar
* Zendesk #2072 - TimedMetadata för AdEvent innehåller inte en fullständig URL bara &quot;http&quot;
* Zendesk #2192 - Bithastigheten är inte alltid lägre vid dåliga nätverksförhållanden
* Zendesk #2256 - Åtkomst till Överordnad Playlist, uppdaterad PSDK för att skicka timedMetadata-händelser för prenumerationstaggar i den överordnad spellistan.
* Zendesk #2269 - Två olika undertextspråk visas på skärmen samtidigt med WebVTT
* Zendesk #2417 - spelaren som försökte hämta undertexter innan uppspelningen startades använde WebVTT fel segmentnummervariabel för segmentnummermatchning. Fel visas bara för media med segmentindex som börjar på noll.
* Zendesk #2470 - PSDK returnerar inte från läget SUSPENDED när bithastigheten ändras efter avstängning. I en speciell situation när smart sökning anropas av RestoreGPUResource (återställ spelaren från pausläge) och strömbrytaren upptäcks tidigare, kan smart sökning inte slutföras och resultera i konstant buffring.
* Zendesk #2451 - dold textning, nedre indrag, added &#39;bottomInset&#39; parameter to caption code
* Zendesk #2480 - inaktivera omdirigering med HTTP 302, utökat stöd för inställning av egenskapen useRedirectedUrl
* Zendesk #2486 - beacons från tredje part
* Zendesk #2547 - Arabiska undertexter: Texten ska justeras högerjusterad

**Version 1.4.4 (1195)**

* Zendesk #1158 - Uppspelningen misslyckas på Huawei Valiant (Y301A1)
* Zendesk #1709 - Felaktig mediestorlek och utsträckt video
* Zendesk #1757 - Endast ljud som spelas upp efter profilväxling mellan strömmar med identiska spa/pps-data
* Zendesk #2095 - HTTP 307-status (omdirigering) gör att Adobe-spelaren stoppar uppspelningen
* Zendesk #2126 - TimedMetaData-händelse saknas för den senaste ADEVENT, prenumerationstaggar som finns efter det sista segmentet rapporterades inte till PSDK från AVE
* Zendesk #2227 - Lockups in VideoEngine nativeReset and nativePause
* Fel 3921755 - uppdatering av OpenSSL-bibliotek till version 1.0.1L

**Version 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - Textning aktiverad och inaktiverad
* PTPLAY-1818 - Spela upp igen stoppas vid annonsen i stället för att spolas förbi den
* PTPLAY-2736 - En tidigare visad WebVTT-bildtext visas på skärmen när en ström med WebVTT-bildtext har spelats klart
* PTPLAY-3773 - En annons för mellanrullning spelas inte upp när direktuppspelningen startas efter annonspositionen

**Version 1.4.2**

* Zendesk #1561 - HLS-klientbaserat failover-stöd i primetime. Använder programdatum och tid för att åtgärda redundans
* Zendesk #1590 - LoadInfo.MediaDuration är alltid 0 (inte fast för enbart ljud)
* Zendesk #1626 - Potentiell minnesläcka i Player. Inte en riktig minnesläcka, problemet var att NotificationHistory sparade de senaste 1 000 meddelandena. Detta har reducerats till 100.
* Zendesk #2192 - Bithastigheten är inte alltid lägre vid dåliga nätverksförhållanden

**Version 1.4.1 (1121)**

* Zendesk #1951 - Lockup in VideoEngine.nativeReset() on 4.0.x devices
* Zendesk #2064 - Native Crash SIGSEGV på specifika intelbaserade Android-enheter
* Zendesk #2075 - Lockup in VideoEngine.nativeReleaseGPUResource on 4.0.x devices
Obs! Denna version är ***obligatoriskt*** för Android 5.0 (Lollipop)
* Zendesk #1513 - Stöd för Android Lollipop
* Zendesk #1709 - Felaktig mediestorlek och utsträckt video
* Zendesk #1871 - WebVTT-bildtexter försvinner ibland och visas sedan igen när du visar en boskap med WebVTT-bildtexter
* Zendesk #1996 - Inga tidslinjemarkörer visas i PSDK 1.4.0
* Zendesk #2046 - Krasch med PSDK 1.4.1.1113, fast krasch för liveströmmar när inga annonser returneras från Audition
* Bug #3769657 - Update the version of curl to 7.38.0
* PTPLAY-1575 - När ABR-uppspelningen börjar med en ström med enbart ljud och sedan växlar till ljud-/videoströmmen återges videon aldrig medan ljudet fortsätter
* PTPLAY-2499 - Uppdatera till OpenSSL till version 1.0.1j för att åtgärda senaste säkerhetsluckor
* PTPLAY-2632 - Videon återskapas inte efter att Ad med mellanrullning är klar på Android Lollipop
* PTPLAY-2678 - Videostopp under live-livetester på Android Lollipop

**Version 1.4.0**

* Zendesk #1024 - Funktion för att ta bort annonser från strömmen via manifest
* Zendesk #1293 - Closed Caption Track Selection Issue.
* Zendesk #1590 - LoadInfo.MediaDuration är alltid 0, mediaDuration visar nu rätt värde.
* Zendesk #1629 - player/app kraschar vid slutet av annonsuppspelning på Galaxy S4
* Zendesk #1674 - ClosedCaption visas inte. Korrigera 708-bildtextvisningen när 0x03 ETX-koder saknas.
* PTPLAY-2157 - Standardformaten för undertextning returnerades av get-metoder, även om olika format har angetts och verifierats visuellt i flödet. Stilegenskaperna för undertexter kommer nu att visa det värde som de har ställts in på.

## Kända fel i 1.4 {#known-issues-in}

**Version 1.4.31**

* PTPLAY-16803 - Textning fungerar inte med enbart ljud eftersom bildtextsystemet behöver video för att fungera. Utan video finns det ingen visningsrutedimension, och utan visningsrutedimension kan vi inte visa någon grafik för bildtexter.
* PTPLAY-1634 - Samma prenumerationstagg har olika tidsstämplar i olika live-fönster. När direktfönstret flyttas bör samma tagg i dem ha samma tidsstämplar. Men ibland har samma taggar olika tidsstämplar.
* PTPLAY-3197 - Krasch med signal 11 SIGSEGV-fel på Acer Iconia-enheten efter ~ 1 timmes kontinuerlig uppspelning
* PTPLAY-3310 - Med lite lägre bithastighet blir ljudet hackigt/hackigt på Acer Iconia
* PTPLAY-3355 - WIN DEATH kraschar på Motorola Xoom med 4.0.x efter ~ 1 timmes kontinuerlig uppspelning.
* PTPLAY-3557 - Om en annonsbrytning spolas tillbaka blir strömmen klar
* PTPLAY-7079 - Uppspelningsfönstret på android-klienten fungerar inte med Secure Stop/Hard Stop
* Fel 3760144 - Upplösningen kan ändras eller se ut att pulsa när strömmen pausas på vissa enheter som Kindle Fire 7 och Samsung Galaxy Nexus. Endast observerbar under noggrann granskning
* Fel 3761170 - seekToLocal i Live med Ads kan inte söka tillbaka till annonsmaterial, det bästa är att använda API:erna currentTime för liveströmmar
* Bug #3763370 - Live-strömmar med annonser visar ibland två annonsmarkörer tillsammans när det bara ska finnas en. Dessa annonsmarkörer representerar samma annons och endast en spelas upp
* Fel 3763373 - Annonsmarkeringen kan försvinna helt kort när du söker förbi en annons i VOD-strömmar. Annonsmarkören återställs och det finns ingen annan negativ effekt på tidslinjen
* Vissa enheter har kända uppspelningsproblem. Se [Kända enhetsproblem i 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Referensimplementering - Trick play implementeras inte i exempelprogrammet
* På vissa Android TV-enheter kan en svart bildruta visas på grund av en avkodningsåterställning vid följande övergångspunkter:
   * in- och utzoomningsläge
   * växla mellan ljudspår med senare bindning
   * från en annons till huvudinnehållet.

**Version 1.4.23**

* Textning fungerar inte med enbart ljud eftersom bildtextsystemet behöver video för att fungera. Utan video finns det ingen visningsrutedimension och utan visningsrutedimension kan du inte visa grafik för bildtexter.
* Från och med version 1.4.23 stöder inte TVSDK Gingerbröd OS 2.3. Detta beror på att TVSDK använde följande privata Android-bibliotek för att samla in maskinvaruinformation om enheter med Gingerbröds operativsystem:

   * `libstagefright.so`
   * `libcutils.so`

I Android N-versionen har Google tagit bort åtkomsten till dessa privata bibliotek. Gingerbröds operativsystem står för närvarande för mindre än 1 % av Android OS-marknadsandelen globalt, så efter version 1.4.23 stöds inte längre Gingerbröds operativsystem av TVSDK.
När du använder version 1.4.23 (som har stöd för Android N) eller senare:
* Uppdatera dina program så att de använder minSdkVersion version 11.
* Om slutanvändaren kör OS 2.3 är SDK-versionen lägre än programmets minSdkVersion. Systemet avbryter programmets installation eller uppgradering.
* Om slutanvändaren kör en version som är senare än OS 2.3 installeras programmet korrekt.

Om du uppdaterar minSdkVersion:

* Om slutanvändaren kör OS 2.3 installeras programmet men uppspelningen fungerar inte.
Detta gäller både uppdatering och installation av ny programvara.
* Om slutanvändaren kör ett system som är högre än OS 2.3 installeras appen korrekt och innehållet spelas upp korrekt.

**Version 1.4.22**

* Den tidiga avslutningen av annonser fungerar inte med vissa annonser i mellanrullen när delnings- och delningstaggen är för nära varandra.

**Version 1.4.2**

* När du spolar tillbaka vid en annonsbrytning slutförs strömmen.

Media Player skickar felaktigt ut MediaPlayer PlayerState.Complete under Trick Play-rewind-åtgärden när den når en annonsgräns. Spelaren bör ignorera den här händelsen i tricks-uppspelningsläge, annars hanteras läget korrekt av SDK.

**Version 1.4.0 (1086)**

* PTPLAY-1634 - Samma prenumerationstagg har olika tidsstämplar i olika live-fönster. När aktiva fönster flyttas bör samma tagg i var och en av dem ha samma tidsstämplar. Men ibland kan även samma taggar ha olika tidsstämplar.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE visas ibland efter flera växlar till/från den alternativa strömmen i strömavbrott
* Fel 3726865 - Om en LBA-ström med MultiBitrate startar från en ström med enbart ljud visas inte videon om den växlas till en ljud-/videoström. Från och med en ljud-/videoström visas inte detta problem och det går att växla mellan ljud- och ljud-/videoströmmar
* Fel 3760144 - Upplösningen kan ändras eller se ut att pulsa när en ström pausas på vissa enheter som Kindle Fire 7 och Samsung Galaxy Nexus. Endast observerbar under noggrann granskning
* Fel 3761170 - seekToLocal in Live with Ads kan inte söka tillbaka till annonsinnehåll; det är bäst att använda API:erna currentTime för liveströmmar
* Bug #3763370 - Live-strömmar med annonser visar ibland två annonsmarkörer tillsammans när det bara ska finnas en. Dessa annonsmarkörer representerar samma annons och endast en spelas upp
* Fel 3763373 - Annonsmarkeringen kan försvinna helt kort när du söker förbi en annons i VOD-strömmar. Annonsmarkören återställs och det finns ingen annan negativ effekt på tidslinjen
* Vissa enheter har kända uppspelningsproblem. Mer information finns i [Kända enhetsproblem i 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Referensimplementering - Trick play implementeras inte i exempelprogrammet.

## Kända enhetsproblem i 1.4 {#known-device-issues-in}

| Enhet | Chipset | Problem | Orsak | Tillfällig lösning |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | ABR-fördröjning förväntas eftersom avkodaren startas om. |  |  |
| HTC Desire (skiljer sig från HTC Desire HD) | QSD8250 | Kan inte spela upp video. Returnerar felet VIDEO_PROFILE_NOT_SUPPORTED. | Önskans maskinvaruavkodare är inte korrekt. Det ger Stagefright&#39;s SW decoder. | Starta om enheten. |
| HTC EVO 4G | QSD8650 | Ingen maskinvaruavkodare. | Qualcomm har ingen maskinvaruavkodare. | Uppgradera till Android 4.x. |
| Kindle FireSystem version 6.0 | TI OMAP4 | Spelar inte upp HLS-strömmar. Video i AIR fungerar inte. |  | Uppgradera till systemversion 6.3. |
| Kindle Fire HD | TI OMAP4 | Kan försättas i ett läge där videon inte kan spelas upp. Returnerar felen VIDEO_PROFILE_NOT_SUPPORTED och UNRECOVERABLE_ERROR. | HW-avkodaren försätts i ett oåterkalleligt läge när programmet inte stänger av HW-avkodaren helt, t.ex. efter att en krasch har inträffat. Händer även i inbyggda appar på enheten. | Starta om enheten. |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE kraschar efter flera ABR-växlar. |  |  |
| Motorola Atrix | Tegra2 | Generella prestandaproblem med AVE jämfört med AIR. Ljud/video ur synk, videouppspelning slutar svara efter uppspelning mellan 9 och 15 minuter. Krascher. | Möjligen relaterat till openGLES som vi aktiverar i AIR. Utredas. |  |
| Nexus 7 (andra generationen) | S4Pro APQ8064 (Qualcomm) | Enheten låser sig när en film pausas i mer än 30 minuter. | Enhetsproblem som har rapporterats till Google. | Appen bör ha en tidsgräns så att den inte tillåter en lång paus. |
| Nexus S (GB) | Humming Bird | Det går inte att spela upp någon video med HW-avkodare. | Det finns ingen Stagefright-baserad HW-avkodare i Nexus S, så för Android 2.3 använder vi en SW-avkodare. | Uppgradera till ICS. |
| Nexus S (ICS) | Humming Bird | Video flimrar ibland. | Felaktiga data kan få avkodaren att hamna i ett felaktigt tillstånd. | Starta om enheten. |
| Nook tabletAndroid OS: 2.3 | TI OMAP 4 | Video spelas inte upp och appen hänger sig. | Stagefright försätts i ett instabilt läge efter att appen har körts några gånger. Anrop till mediaplayer::QueryCodecs låser sig. | Starta om enheten för att återställa tillståndet. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | Det går inte att installera programmet SampleMediaPlayer. | Använder ARM v6 i stället för den vanligare ARM v7-kretsuppsättningen. FP/AIR stöder inte den här enheten. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | Kan inte spela upp video. | Den här kretsuppsättningen är en okänd avkodare för Android pre-ICS i AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | Videoprestanda är inte upp till parvis för den här enheten. | HW-avkodaren returnerar avkodade bildrutor med fel PTS. Det verkar som om avkodaren använder avkodningstid i stället för presentationstid. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | TI OMAP4 | Kraschar vid start av video. |  | Uppgradera till Android 2.3.7 eller 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | Ibland slutar videon att svara och bara ljud spelas upp. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | Videon fryser. | Undersöker. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | MBR-övergång kan ta upp till tre sekunder. | Som en korrigering för MBR-krascher startar vi om avkodaren för varje strömbrytare, vilket kan ta upp till tre sekunder. |  |
| Samsung Galaxy Y |  | Det går inte att installera programmet SampleMediaPlayer. | Använder ARM v6 i stället för den vanligare ARM v7-kretsuppsättningen. FP/AIR stöder inte den här enheten. |  |
| Xoom | Tegra | Några bildrutor tas bort för växling. Avkodaren har inte startats om. | OMXAL-begränsning. |  |

## Användbara resurser {#helpful-resources}

* Läs den fullständiga hjälpdokumentationen på [Adobe Primetime Learn &amp; Support](https://helpx.adobe.com/support/primetime.html)-sidan.
