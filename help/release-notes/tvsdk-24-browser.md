---
title: Versionsinformation för Browser TVSDK 2.4
description: Versionsinformationen för Browser TVSDK 2.4 beskriver de nya funktionerna som stöds och inte stöds samt de kända problemen i Browser TVSDK 2.4.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# Versionsinformation för Browser TVSDK 2.4 {#browser-tvsdk-release-notes}

Versionsinformationen för Browser TVSDK 2.4 beskriver de nya funktionerna som stöds och inte stöds samt de kända problemen i Browser TVSDK 2.4.

## Introduktion {#introduction}

Browser TVSDK är en verktygslåda som gör att du kan lägga till avancerade videouppspelningsfunktioner, innehållsskydd och annonsering i webbläsarbaserade videospelarprogram.

Browser TVSDK 2.4 innehåller JavaScript-API:er för att bygga webbläsarbaserade videoprogram och inkluderar uppspelningsstöd i följande lägen:

* Endast HTML5
* HTML5 med autoblixt som reserv
* Flash alltid

Den här versionen innehåller följande information:

・ [Dokumentation för webbläsarens TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

・ [Programmeringshandbok för webbläsare TVSDK](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

・ [TVSDK for 1.4 DHLS to Browser TVSDK 2.4 Migration Guide](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

・ [Konvertera från webbläsare TVSDK 2.4.6 till version 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

・ En referensimplementering som ingår i bygget.

>[!NOTE]
>
>*En fullständig lista över säkerhetsaspekter för den här versionen finns i Säkerhetsfrågor.

## Nyheter och funktioner {#what-s-new-and-supported-features}

I den här versionen av Browser TVSDK finns nya funktioner som du kan använda för att förbättra dina videoprogram.

**Nytt i 2.4.12-uppdateringen (build 2014)**

Följande tillägg finns som en del av Browser TVSDK 2.4.12 Update (Build 204):

* Implementeringen av volym-API för AdobePSDK.MediaPlayer ändras så att automatisk uppspelning tillåts på iOS när uppspelningen stängs av.

・ Ett nytt API, `auditudeSettings.ignoreVPAIDAds`, läggs till för att tillåta ignorering av VPAID-annonser som tagits emot från Auditude-servern. API:t fungerar inte för Flash Fallback.

**Version 2.4.11**

Följande förbättringar och tillägg finns i Browser TVSDK 2.4.11:

・ HLS Live-segmentredundans stöds för MSE och Flashens grundlägen.

・ Stöd för `AuditudeSettings.creativeRepackagingDomain` API finns nu även för MSE. Tidigare hade det bara stöd för Flashens reservläge.

・ Versionen innehåller korrigeringar för allvarliga kundproblem. Se *Åtgärdade problem* en lista.

**Version 2.4.10**

Följande förbättringar och tillägg finns i Browser TVSDK 2.4.10:

・ TVSDK tillhandahåller enableLogging() för att aktivera eller inaktivera loggningen. Se [API-dokumentation](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)för användning.

・ TVSDK stöder inte längre standardkapitel när Adobe Analytics används. Definiera och hantera kapitel med ditt program.

・ Versionen innehåller korrigeringar för allvarliga kundproblem. Se *Problem har åtgärdats *en lista.

**Version 2.4.9**

Följande förbättringar och tillägg finns i Browser TVSDK 2.4.9:

・ HLS VOD- och Live-strömmar med tidsavbrott men utan kontinuitetsmarkörer stöds.

・ ID3 v2.4.0-bildrutor stöds med Safari-videotaggen för HLS VOD- och Live-strömmar.

・ Implementering av säker annonsinläsning säkerställer att annonsserveranrop uppgraderas för att skydda HTTP baserat på API-konfiguration. Mer information finns i klasserna AdobePSDK.AdvertisingMetadata och AdobePSDK.ForceHttpsAdConfiguration. Den här funktionen stöds inte i Flashens grundläge.

・ Information om annonserings-ID och tilläggsinformation som hör till VAST 3.0-svar är nu tillgängliga för programmet av TVSDK och kan användas för att implementera Moat-integrering för annonsmätningar. Mer information finns i API:t för AdobePSDK.NetworkAdInfo. Detta stöds inte i Flashens grundläge.

・ Klassen AdobePSDK.ForceHttpsConfiguration är inte längre tillgänglig. Den slutförs av

Klassen AdobePSDK.ForceHttpsAdConfiguration.

・ Ett nytt API, AdobePSDK.optimizeFlashCall, finns nu tillgängligt för att optimera anropen för att förbättra uppspelningen av HLS i Flashens fallback-läge. Detta är inaktiverat som standard.

**Nytt i 2.4.8-uppdateringen (build 6002)**

Den här uppdateringen innehåller korrigeringar för viktiga kundproblem. Se *Åtgärdade problem*, för listan.

**Version 2.4.8**

Följande förbättringar och tillägg finns i Browser TVSDK 2.4.8:

・ SDK är nu kompatibelt med Chrome EME och de bästa metoderna som är tillgängliga från och med Chrome v58. Mer information finns i [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

・ UI Framework har nu stöd för HLS Access DRM i arbetsflödet Flash, endast annons och målinfo.

・ API:t setDRMAuthenticateData läggs till i UI Framework. Anropa detta API om du vill spela upp strömmar som skyddas med Adobe Access-DRM. Attributet drmAuthenticateData kan också anges i spelaren. Se [AdobePSDK.videoBehavior](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)för mer information.

**Version 2.4.7**

Följande funktioner är nya i version 2.4.7:

・ Tillägg av gränssnittskonfiguratorn i gränssnittsramverket

Du kan konfigurera spelaren på något av följande sätt:

・ Använda ett JSON-objekt

・ Använda API

Browser TVSDK har ett **UI Configurator **verktyg som hjälper dig att generera JSON-objektet.

I det här verktyget kan du välja olika inställningar, klicka på **Testa konfiguration **för att verifiera inställningarna och klicka på **Hämta konfiguration **för att hämta inställningarna. När du har hämtat filen kan du skicka innehållet i filen som JSON-objekt till API:t ptp.videoPlayer.

・ MediaPlayerItemConfig-API:t har lagts till i gränssnittsramverket

Olika funktioner, som advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration, kan konfigureras med MediaPlayerItemConfig. Mer information finns i dokumentationen för AdobePSDK.MediaPlayerItemConfig i [Webbläsare-TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [dokumentation](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

I UI Framework har sättet att skicka nätverkskonfigurationer via spelarkonfigurationen ändrats.

**Version 2.4.6**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`networkConfiguration: <network configuration object>`

`}`

`};`

**Version 2.4.7**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`mediaPlayerItemConfig: {`

`networkConfiguration: <network configuration object>`

`}`

`}`

`};`

* Stöd för DRM- och analysarbetsflöden i UI-ramverket

DRM-konfigurationer och Analytics Tracking kan aktiveras via UI Framework.

* Tillägg av `AdobePSDK.embedSWFinFullScreenDiv` API

Det nya API:t ger spelarappen flexibilitet att välja den div som den kan bädda in filen FlashFallback.swf i.

* Ersatt `getVersion`API från `AdobePSDK.MediaPlayer` klass med `AdobePSDK.Version` för TVSDK-versionsrelaterad information. Mer information finns i `AdobePSDK.Version` API [här](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Version 2.4.6**

Följande funktioner är nya i version 2.4.6:

* **Stöd för Browserify**

Med Browserify kan du använda nod.js-formatmodulerna i webbläsaren. Du kan definiera beroenden och Browserify paketerar allt i en JavaScript-fil.

* **Fakturering**

Med hjälp av fakturering kan Browser TVSDK samla in användningsstatistik för spelare för att ta betalt av Primetime-kunder.

>[!NOTE]
>
>Den inaktuella uppräkningen MediaPlayer.Events och inaktuella konstanter i Enum PSDKErrorCode har tagits bort i version 2.4.6. Mer information finns i [Konvertera från webbläsare TVSDK 2.4.5 till version 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Version 2.4.5**

Följande funktioner är nya i version 2.4.5:

* **Full Event Replay and Ads**

  HLS FER-strömmar (Full Event Replay) har nu stöd för annonsupplösning och annonsbeteenden. Om du vill aktivera det här stödet anger du att annonssignaleringsläget ska vara `MANIFEST_CUES` när du skapar `MediaPlayerItemConfig` -objekt.

* **MediaplayerView ScalePolicy Support**

  Programutvecklare kan nu ange en annan scalePolicy för vyn med egenskapen scalePolicy i MediaplayerView.

* **Stöd för anamorfiskt innehåll**

  Uppspelning av anamorfiskt innehåll stöds nu när MSE och Flash används.

* **Selektiv tillämpning av`withCredentials`**

När `withCredentials` är inställd på true, `Access-Control-Allow-Origin` kan inte anges till ett jokertecken. Beroende på serverns svar kommer webbläsare-TVSDK att välja vilken inställning som ska användas `withCredentials` -attribut. Mer information om det här stödet finns i [Webbläsarens TVSDK API-dokument](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Version 2.4.4**

Följande funktioner var nya i version 2.4.4:

* **Exempelappen Chromecast**

Den här versionen har stöd för en avsändare- och mottagarapp som demonstrerar uppspelning av DASH VOD-strömmar och DASH Widewin-strömmar med annonsinfogning på klientsidan.

* **Avancerat stöd för failover**

Den här versionen innehåller stöd för avancerade failover-användningsfall (segment och serverfailover) för HLS VOD-strömmar.

**Version 2.4.3**

Följande funktioner var nya i version 2.4.3:

* **Anpassade taggar för DASH VOD**

  Textbundna anpassade taggar (händelser) kan prenumereras på och tas emot som TimedMetadata-objekt.

* **Uppspelning av strömmar utan tillägg**

  HLS- och DASH-strömmar utan tillägg stöds nu. För manifestfilen måste resourceType anges när resursen läses in. För segment och VTT-filer används Content-Type-svarshuvudet för att avgöra innehållstypen.

**Version 2.4.2**

Följande funktioner var nya i version 2.4.2:

* **API-paritet**

En fullständig lista över API-pariteten finns i [TVSDK for 1.4 DHLS to Browser TVSDK 2.4 Migration Guide](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Stöd för Sample-AES**

  Den här versionen har stöd för Sample-AES-krypterad innehållsuppspelning på MSE och Flashens reservlösningar. Kravet på att lagra AES-innehåll över säkert ursprung i Google Chrome har tagits bort.

* **Stöd för AAC-behållare**

  Uppspelning av filer med tillägget .aac stöds nu. Detta kan vara strömmar med enbart ljud eller alternativt ljud.

  >[!NOTE]
  >
  >AC3 och förbättrade AC3-kodekar stöds ännu inte.

* **Uppspelning av tokeniserad ström**

HLS-strömmar som levereras via ett CDN (Content Delivery Network) kan ibland använda autentiseringstoken för manifest- och segmentbegäranden för verifiering, och dessa tokens kan anges som URL-parametrar eller som cookie-rubriker. Uppspelning av sådana strömmar stöds nu.

**Version 2.4.1**

Följande funktioner var nya i version 2.4.1:

* **Gränssnittsramverk**

Det här ramverket, som är utformat för att snabba upp gränssnittsutvecklingen för JavaScript-baserade videospelarprogram, består av API:er för att inkludera grundläggande kontroller som play/pause och volume samt för att enkelt lägga till eller ta bort element som scrub bar-lägen och inställningar för stängd bildtext. Du kan ange beteendet som är kopplat till kontroller, skapa anpassade kontroller och skalförändra spelarens användargränssnitt. Allt detta sker i ramverket, utan att DOM-strukturen behöver ändras direkt.

* **Förbättrad HLS-uppspelning för liveströmmar**

Den här versionen stöder avbrott orsakade av annonsinfogning. Den använder taggen EXT-PROGRAM-DATE-TIME följt av taggen EXT-MEDIA-SEQUENCE för att synkronisera olika bithastighetsprofiler för smidig uppspelning.

* **Stöd för VPAID 2.0**

VPAID (Video Player ad-service interface definition), version 2.0, ger en multimedieupplevelse för användarna och gör det möjligt för utgivare att bättre rikta annonser, spåra annonsvisningar och tjäna pengar på videoinnehåll. Den här versionen har stöd för linjära VPAID-annonser i JavaScript för VOD-innehåll (video on demand).

* **Anpassade HLS-taggar**

Medieströmmar kan innehålla ytterligare metadata i form av taggar i spellistan/manifestfilen. Med Browser TVSDK kan du ange och prenumerera på ytterligare taggar och få meddelanden när dessa taggar visas i manifestet.

* **Annonsmarkörer som visas på spelarens tidslinje**

Den här versionen har stöd för att visa annonsmarkörer på spelarens tidslinje för både VOD- och Live-innehåll. Du kan se detta beteende i referensspelaren.

**Stöds i 2.4**

Följande funktioner fanns i version 2.4:

* **MP3-ljuduppspelning**

  Den här versionen stöder MP3-ljuduppspelning i webbläsare med Media Source Extensions (MSE) och med videotaggen Safari.

* **MP4-videouppspelning**

  Följande funktioner stöds:

   * Enkel direktuppspelning
   * Pre-roll och Post-roll MP4-annonser med annonsbeteenden och spårning
   * HLS-annonser före och efter rullning med annonsbeteenden och spårning
   * DASH-annonser före och efter rullning med annonsbeteenden och spårning

## Plattformar som stöds {#supported-platforms}

Browser TVSDK har specifika krav för de plattformsnivåer och den programvara som ska köras. Följande plattformar och programnivåer stöds:

### Konfigurationer för datorer {#desktop-configurations}

* Microsoft Windows 7:

   * Internet Explorer 11+
   * Krom 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Krom 33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* APPLE OS X

   * Safari 9+
   * Krom 33+
   * Firefox 38+

### Webbkonfigurationer för mobiler {#mobile-web-configurations}

* Android 4.4

   * Inbyggd webbläsare
   * Krom 33+

* Android 5.0

   * Inbyggd webbläsare
   * Krom 33+

* Android 6.0

   * ・ Chrome 33+

* APPLE IOS 9

   * Safari 9+
   * Krom 33+

* Apple iOS 10

   * Safari 9+
   * Krom 33+

**Google Chromecast (andra generationen; endast för DASH-uppspelning)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Teknik</strong> </p> </td> 
   <td><p><strong>Videotagg för webbläsare: TVSDK</strong><sup>1</sup></p> </td> 
   <td><p><strong>Webbläsare: TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>Standardteknik</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4 och HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>Videotagg</p> </td> 
  </tr> 
  <tr> 
   <td><p>Android</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS och DASH</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple Safari 8</p> </td> 
   <td><p>MP4 och HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 och HLS</p> </td> 
   <td><p>Videotagg</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS och DASH</p> </td> 
   <td><p>MP4 och HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS och DASH</p> </td> 
   <td><p>MP4 och HLS</p> </td> 
   <td><p>MSE<sup>2</sup></p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 7)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 och HLS</p> </td> 
   <td><p>Flash</p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 8.1)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS, DASH</p> </td> 
   <td><p>MP4 och HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## Funktionsmatris {#feature-matrix}

Här är en lista över funktioner som stöds och inte stöds i den här versionen:

* *Funktioner för MP3-ljud - Core Playback*
* *MP4-videofunktioner - Core Playback*
* *MP4-videofunktioner - Core Ad Insertion*

>[!NOTE]
>
>*I funktionens matristabeller nedan betyder &quot;Y&quot; att funktionen stöds i den aktuella versionen.*

### MP3-ljudfunktioner {#mp-audio-features}

**Tabell 1: Kärnuppspelning{#table-core-playback}**

| Kategori | Innehållstyp | Funktion | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Uppspelning | MP3 VOD | Allmän uppspelning (Spela upp, Pausa, Sök) | Stöds inte | Y | Y |

1 Taggen Browser TVSDK Video stöder inte direktuppspelning och DRM. Stödet för kodek och behållare är inte detsamma i alla webbläsare.

2 Firefox har standardvärdet Flash Player för version 41 eller tidigare.

### Funktioner för MP4-ljud {#mp-audio-features-1}

**Tabell 2: Kärnuppspelning**

| Kategori | Innehållstyp | Funktion | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Uppspelning | MP4 VOD | Allmän uppspelning (Spela upp, Pausa, Sök) | Stöds inte | Y | Y |

**Tabell 3: Core Ad Insertion**

| Kategori | Innehållstyp | Funktion | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | Förrullning (MP4) | Stöds inte | Y | Y |
| Ad Insertion | MP4 VOD | Efterrullning (MP4) | Stöds inte | Y | Y |

Mer information om stöd för HLS- och DASH-funktioner finns nedan.

## HLS-funktionsmatris {#hls-feature-matrix}

Här är funktionsmatrisen för HLS-funktionerna i Browser TVSDK.

* *HLS Core-uppspelning*
* *HLS Avancerade uppspelningsfunktioner*
* *Funktioner för skydd av HLS-innehåll*
* *HLS Core och infogningsfunktioner*
* *HLS Avancerade funktioner för annonsinfogning*
* *HLS-integrering*

>[!NOTE]
>
>*I funktionens matristabeller nedan betyder &quot;Y&quot; att funktionen stöds i den aktuella versionen.*

### HLS-funktioner {#hls-features}

Följande funktioner stöds:

**Tabell 4: Uppspelning av HLS Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Allmän uppspelning (play, pause, seek)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Allmän uppspelning (spela upp, pausa och söka)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adaptiv bithastighet</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708 bildtexter</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Endast VOD</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Manifestväxling vid fel</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Avancerad redundans</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>QoS och spelarmeddelanden</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Begränsat QoS-stöd</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Stöd för cookie-rubriker</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Ange parametrar för buffertkontroll</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Ange adaptiv</p> <p>bithastighetskontroller</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Egna taggar</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td>Ljud med låg bindning</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302 omdirigering</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 5: Avancerade HLS-uppspelningsfunktioner**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Uppspelning vid förskjutning</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Uppspelning med endast ljud</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Trick Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Smidig testkörning</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3-parsning</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Stöd för brytpunkter</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Tokeniserade strömmar</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Fakturering</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 6: Funktioner för skydd av HLS-innehåll**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Skydd av innehåll</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Skydd av innehåll</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Skydd av innehåll</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Adobe Access</p> </td> 
   <td><p>Stöds inte</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 7: HLS Core och infogningsfunktioner**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Förrullning (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Efterrullning (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Annonsupplösning och beteenden</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Standardannonspolicy</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Creative Repackaging (MP4 to HLS)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 8: Avancerade HLS-annonsinfogningsfunktioner**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Endast annons</p> </td> 
   <td><p>Stöds inte</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Målparametrar</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Egna parametrar</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Anpassad annonspolicy</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Lazy och laddning</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Stöds inte</p> </td> 
   <td><p>Plattformsbegränsning</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Pressmeddelanden, banners, klickbara annonser</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 9: HLS-integrering{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integreringar</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Integrering med Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## DASH-funktionsmatris {#dash-feature-matrix}

Här är funktionsmatrisen för DASH-funktionerna i Browser TVSDK.

・ *Uppspelningsfunktioner för DASH Core*

・ *Avancerade uppspelningsfunktioner för DASH*

・ *Skyddsfunktioner för DASH-innehåll*

・ *Funktioner för annonsinfogning i DASH Core*

・ *Avancerade funktioner för annonsinfogning i DASH*

・ *DASH-integreringar*

>[!NOTE]
>
>I funktionsmatristabellerna nedan betyder ett Y att funktionen stöds i den aktuella versionen.

### DASH-funktioner {#dash-features}

Följande funktioner stöds:

**Tabell 10: Uppspelningsfunktioner för DASH Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>HTML 5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Allmän uppspelning (play, pause, seek)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Allmän uppspelning (spela upp, pausa och söka)</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adaptiv bithastighet</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708 bildtexter</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Redundans</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>QoS och spelarmeddelanden</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Stöd för cookie-rubriker</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Ange parametrar för buffertkontroll</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Ange adaptiva bithastighetskontroller</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Anpassade taggar (EventStream)</p> </td> 
   <td><p>Endast VOD (intern)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Ljud med senare bindning</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302 omdirigering</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 11: Avancerade DASH-uppspelningsfunktioner**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><strong>HTML 5 FF, IE, Chrome, Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Uppspelning vid förskjutning</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Uppspelning med endast ljud</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Trick play</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Smidig testkörning</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3-parsning</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Stöd för flera perioder</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Tokeniserade strömmar</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
  <tr> 
   <td><p>Uppspelning</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Fakturering</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 12: Skyddsfunktioner för DASH-innehåll**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>HTML 5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Skydd av innehåll</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
  <tr> 
   <td><p>Skydd av innehåll</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
  <tr> 
   <td><p>Skydd av innehåll</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>・ Bredd på Chrome, Firefox 47 och senare samt Chromecast</p> <p>・ PlayReady i Internet Explorer i Windows 8.1 och Edge</p> <p>・ Primetime DRM för Windows Firefox (endast video)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 13: Funktioner för infogning av DASH Core-annonser**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>HTML 5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Förrullning (MP4/DASH)</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (DASH)</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Efterrullning (MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Annonsupplösning och beteenden</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Standardannonspolicy</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Creative Repackaging (MP4 to DASH)</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 14: Avancerade funktioner för DASH-annonsinfogning**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Endast annons</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Målparametrar</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Egna parametrar</p> </td> 
   <td><p>Endast VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Anpassad annonspolicy</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Lazy och laddning</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Pressmeddelanden, banners, klickbara annonser</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>Stöds inte</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 15: DASH-integreringar**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Kategori</strong></p> </td> 
   <td><p><strong>Innehållstyp</strong></p> </td> 
   <td><p><strong>Funktion</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integreringar</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Integrering med Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Åtgärdade problem {#issues-fixed}

**Problem som har korrigerats i uppdatering 2.4.12 (build 204)**

Följande problem har åtgärdats i Browser TVSDK version 2.4.12 Update (Build 204):

・ **21647**- TVSDK bör tillåta automatisk videouppspelning på iOS-enheter när ljud stängs av.

・ **21465**- Åtkomst nekad till felnyckelsystem tas emot när en DRM-skyddad DASH-ström spelas upp efter att en DASH Live-ström spelats upp.

・ **21442**- Aktivera automatisk uppspelning av innehåll på iOS Web när annonsen har spelats upp med en användargest.

・ **21240**- Tillhandahålls API för att filtrera VPAID-annonser som tolkas från Auditude/VMAP.

**Problem som har korrigerats i version 2.4.11**

Följande problem har åtgärdats i Browser TVSDK version 2.4.11:

**Kärnfunktioner för uppspelning:**

・ **19192**: TVSDK implementerar nu TextFormat:bottomInset och TextFormat:safeArea. På grund av dessa förbättringar kan undertexter placeras om om om kontrollfältet visas på skärmen.

・ **21009**: Undertexter finns kvar på skärmen vid sökning efter avbrott tills nya undertexter visas.

・ **21141**: Sökning tillbaka nekas på grund av ett konkurrensvillkor under segmenttillägg.

・ **21142**: Göra sökbara uppspelningsintervall tillgängliga när spelaren är i INITIALIZED-läge. På grund av dessa ändringar stöds nu start-session vid position.

・ **21363**: 608/708 undertexter håller på att bli osynkroniserade efter annonsinfogning för DASH-strömmar.

**Funktioner för annonsinfogning:**

・ **21179**: Problem som rör flera rader (långa pauser, svarta bildrutor) med VOD-innehåll löses nu genom att egenskapen ad.primärAsset.adParameters ställs in korrekt.

・ **21257**: MP4-filen med den högsta bithastigheten markeras för omkodning om MP4 inte är en giltig MIME-typ och den kreativa ompaketeringsfunktionen är aktiverad.

・ **21361**: TVSDK skickar nu annonssystem och kreativt ID från VAST-svaret som frågeparametrar i den kreativa paketeringsbegäran för att stödja ytterligare normaliseringsregler.

**Problem som har korrigerats i version 2.4.10**

Följande problem har åtgärdats i Browser TVSDK version 2.4.10:

**Kärnfunktioner för uppspelning:**

・ **21060**: Ogiltigt codec-fel genererades med HLS-strömmar som innehåller avbrott och ISO BMFF-rutorna körs till slutet av strömmen.

・ **21045**: Automatisk uppspelning fungerar inte på iOS när den första videouppspelningen i en spelningslista har slutförts.

・ **20975**: Bildrutefrekvensen returneras som NaN av QoS-providern i webbläsaren Chrome.

・ **20823**: Ett codec-fel utan stöd utlöses när segment utan data påträffas.

・ **20769**: SDK börjar nu med den aktuella bithastigheten vid sökning i stället för att omedelbart växla baserat på ABR-principen.

・ **20031**: I stående läge på IE11 (Windows 8.1) blir videobilden liten. Funktion för innehållsskydd:

・ **19316**: Hoppa över segment som inte kan dekrypteras vid HLS AES-128-strömmar.

**Problem som har korrigerats i version 2.4.9**

Följande problem har åtgärdats i Browser TVSDK version 2.4.9:

**Kärnfunktioner för uppspelning:**

・ **13407**: DASH-strömmar kan stoppas om Firefox slutar skicka händelsen ontimeupdate under uppspelning.

・ **16380**: Vid uppspelning av multiplexat ljudvideoinnehåll för segment som inte matchar starttiderna via MSE ackumuleras ljudsynkroniseringsfel mellan representationer på ABR-växlar, vilket i slutänden resulterar i ett fel (Chromium-problem nr 663686).

・ **17985**: Vid uppspelning av en viss ISO-BMFF-ström i Firefox-webbläsaren fastnar uppspelningen (Firefox-problem nr 1342913). Detta har åtgärdats sedan Firefox v53.

・ **19141**: Ej infångad (i utlovat) ReferenceError: bredden har inte definierats.

・ **18997, 19299**: Problem med videoflimmer vid segmentgränsen. Detta inträffade eftersom SDK inte räknade ut det senaste samplets tidskompositionsförskjutning korrekt.

・ **19780**: Uppspelningen startar inte för HLS-innehåll och HLS-annonser i Firefox v53 (Firefox-utgåva nr 354653).

・ **20046**: Datum och tid för program tas emot som nyckel i stället för som värde när det tas emot som tidsbestämda metadataobjekt.

・ **20047**: useDefaultResizeHandler returnerar ett fel med Flashens reserv.

・ **20179**: Flash Fallback fungerar inte med Flash Player v25.0.0.171.

・ **20293**: Firefox stoppar buffring av data för vissa HLS-strömmar vilket leder till att data stannar.

・ **20626**: Spelaren genererar ett mediadekodningsfel i Chrome på grund av felaktig hantering av videosamplingar utan varaktighet.

・ **20078**: Uppspelningen stoppas vid webbläsarfel &#39;QuotaExceeded&#39;.

・ **18639**: I HLS Live-ström 608 CC visas ibland felstavad text.

・ **20028**: Storleksparametern ClosedCaptions ändrar inte teckenstorleken.

・ **20613**: Undertexter överlappar varandra vilket gör dem oläsliga.

**CSAI-funktioner (Core Ad Insertion):**

・ **20043**: Annonsintrycket saknas och annonsuppföljningsanrop med flera annonser och omdirigeringar från tredje part saknas.

・ **20044**: När du använder automatisk ompaketering måste alla annonser i annonsuppbrytningen packas om korrekt, annars ignoreras alla annonsuppbrytningar.

・ **20097**: Annonsuppspelning hoppas över och huvudinnehållet återupptas omedelbart i stället för att vänta på en timeout på 20 sekunder om inget annonsmanifest är tillgängligt.

**Problem som har korrigerats i version 2.4.8 Update (build 6002)**

Följande problem har åtgärdats i Browser TVSDK version 2.4.8 Update (Build 6002):

・ **14126:** Uppspelningen kan stoppas i Firefox (utgåva 1316024) på grund av den interna luckan i MSE-källbufferten. Försök att söka för att återuppta uppspelningen

・ **19608** Korrigera för att följa tidsförskjutningsvärdet från Auditude VMAP-svaret.

・ **19635** Korrigerar videohögen i Internet Explorer 11 i Windows 10.

・ **19761** Korrigeringar för ABR-problem med HLS.

・ **19780** Korrigerar annonsuppspelningen med HLS-innehåll som har brutits i Mozilla Firefox v53.

・ **1987 och 19744:** Problemen åtgärdar inkonsekvensen i val av bithastighet efter en sökåtgärd. Nu är bithastigheten som väljs vid sökning det lägre värdet för den aktuella bithastigheten och bithastigheten vid starten.

・ **1981:** Uppspelningen sitter fast och buffringsövertäckningen visas oändligt länge efter att sökningen har utförts i 3-4 gånger.

・ **1984:** Bekräfta överensstämmelse med kraven för betaversionen av Chrome 59 VMP (Beta Verified Media Path). bTVSDK kunde spela upp DRM-innehåll av typen Widewin med Chrome 59 Beta.

・ **19916** DRM-uppspelningen i UI-Framework avbröts. Nu anropas obtainLicense även om det inte finns någon princip i metadata.

**Problem som har korrigerats i version 2.4.8**

Följande problem har åtgärdats i Browser TVSDK 2.4.8:

・ **10075**: Vid sökning i förväg på tidslinjen togs inte händelsen play complete emot i Firefox och Chrome och seek togs inte emot i Firefox.

・ **15775**: En händelse om slutförd uppspelning togs inte emot i Internet Explorer för Windows 8.1.

・ **17306**: För SSAI-strömmar stöds uppspelning. Spårning av sammanfogade bilder stöds inte.

・ **19142**: Ibland gör tillbakaspolning att videouppspelaren förblir i buffertläge för alltid.

・ **19218**: Annonsmarkörer är inte tillgängliga via gränssnittets ramverk.

・ **19219**: Ads only playback fungerar inte via UI-ramverket.

・ **19222**: AES-128-nyckeln begärs en gång för en spelningslista och efterföljande begäranden hanteras från cachen. Tidigare begärdes det för varje segment.

・ **19597**:&quot;TypeError utan infångning: Det går inte att läsa egenskapen &#39;log&#39; för undefined&#39; i Chrome Canary-byggen.

・ **19605**: adRequestDomain var inte tillgängligt i Flashens återställningsläge.

・ **19608**: VMAP-annonser infogades inte för HLS Live-strömmar. SDK hanterar nu referenspunkter och förlitar sig inte på tidsförskjutningsvärden i VMAP-svar.

・ **19637**: Ads only playback leder till skriptfel i slutet av annonsen.

・ **19732**: Begäran om CRS-spelningslista misslyckades med 404-fel. Begärandena 1401 och 1403 från Browser TVSDK uppdateras nu för att hantera detta.

・ **19762**: obtainLicense anropades tidigare före setAuthenticationToken för vilken en giltig licens returnerades oavsett tokengiltigheten. Detta är nu åtgärdat och obtainLicense anropas endast efter setAuthenticationToken-svar.

**Problem som har korrigerats i version 2.4.7**

Följande problem har åtgärdats i version 2.4.7:

・ **8397**: HLS Live-strömmar som genereras via Adobe Media Server kanske inte spelas upp om segmenten inte börjar med en nyckelbildruta.

・ **13606**: Flera sökrelaterade problem har korrigerats för HLS-ström i Chrome-webbläsaren.

・ **14807**: I webbläsaren Chrome, om seek eller pause aktiveras omedelbart efter play(), kan uppspelningen stoppas med felet DOMException: play()-begäran avbröts av ett anrop... (Chromium-problem nr 593273).

・ **19085**: MediaPlayer-parametrar som volume, abrControlParameters och ccStyle är inte inställda på Defaults när Player återställs.

**Problem som har korrigerats i version 2.4.6**

Följande problem har åtgärdats i version 2.4.6:

・ **18093**: TimedMetadata för taggen bredvid taggen subscribed returneras när du använder Flash Player version 24 i Flash Fallback-läge.

**Problem som har korrigerats i version 2.4.4**

Följande problem har åtgärdats i version 2.4.4:

・ **8711**: I MSE är bildtexter 608/708 som standard vänsterjusterade.

・ **13934**: ABR-inställningar för annonser kan inte användas vid uppspelning med HLS Live-strömmar.

・ **14079**: Längdhet för HLS Live-strömmar med lågt DVR-fönster kan misslyckas eftersom uppspelningen kan hamna på efterkälken på grund av problem med nätverksfördröjning. Klicka på live-punkten för att återuppta uppspelningen.

・ **15037**: De exempel som levereras med spelarens gränssnittsramverk fungerar inte i Microsoft Internet Explorer 10 i Windows 7.

・ **15913**: För HLS VOD-strömmar spelas inte strömmen upp i Chrome om manifestsvaret är 304 som inte ändras. Detta har åtgärdats sedan Chrome v55 (Chromium issue 633696).

・ **16103**: I Android Chrome kan uppspelningen under förhållanden med låg bandbredd avbrytas med Uncaught TypeError: Det går inte att läsa egenskapen programDateTime för odefinierat fel.

・ **16265**: För HLS VOD- och Live-strömmar fungerar inte sökning efter avbrott.

・ **16709**: Om du återupptar HLS Live-strömmen med PDT och avbrottsmarkören kan spelaren hamna i buffring.

## Kända fel och begränsningar {#known-issues-and-limitations}

Begränsningarna och kända fel i Browser TVSDK anges nedan.

**Tabell 16: Kärnfunktioner för uppspelning**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Innehållstyp</strong></td> 
   <td><strong>Funktion</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML 5 i Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 i Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (endast DASH-uppspelning)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Allmän uppspelning (Spela upp, Pausa, Sök)</td> 
   <td><p>・ Andra medieformat än HLS stöds inte.</p> <p>8799: Flashens reservlösningar tar inte hand om blandat innehåll och därför måste det säkerställas att innehåll, annons och andra URL:er inte leder till blandat innehåll (säkert och osäkert innehåll tillsammans).</p> <p>・ 19271: Multivisningsuppspelning via UI-ramverket stöds inte i Flashens fallback-läge.</p> <p>・ Återställning efter Flash fungerar inte i Microsoft Internet Explorer 8 och 9 i Windows 7 eftersom dessa versioner inte stöds av SDK:n.</p> <p>・ 20262: Flashens reserv lägger till anpassade parametrar i informationslistan för mål. Även prioritetsordningen för anpassade parametrar skiljer sig åt när det gäller Flash och MSE.</p> <p>・ 20653: Webbläsarens TVSDK-Flash fungerar inte med Win10 med Creators Update.</p> <p>・ Flash Fallback fungerar med Flash Player version 23 och senare.</p> <p>・ 20087 - Beta för Chrome 59 med</p> <p>Flash 25.0.0.171</p> <p>Beta (standard) fungerar inte HLS-uppspelning i läget Flash Fallback. Det fungerar bra på Canary.</p> </td> 
   <td><p>・ 12563: Streckbilder med ljudkodeken mp4a.40.02 spelas inte upp i Firefox på grund av att ljudkodeksträngen i MPD inte stöds. Ljudkodek mp4a.40.2 stöds.</p> <p>15029: När du växlar mellan videoklipp i multiView i UI-Framework uppdateras inte knappen för uppspelning/paus korrekt.</p> <p>・ 16034:I Windows 8.1 IE leder anrop av reset() till ett okänt MIME-typfel. Läs in mediet igen för att återuppta uppspelningen.</p> <p>・ 18235: Vissa sökproblem har observerats med DASH-strömmar med annonser.</p> <p>・ 18727: Fel-API stöds inte för MSE</p> <p>18750: Statusändringshändelser kanske inte är i ordning i vissa fall för både SDK- och UI-ramverket och i UI-ramverket saknas IDLE- och Initializing StatusChange-händelser för händelseavlyssnare som läggs till efter att resursen har lästs in.</p> <p>・ 18889: Om MediaPlayer är i FEL-läge returneras inte visningsobjektet.</p> <p>・ 19039: Om AdobePSDK. MediaPlayer. seekToLocal() används med ett värde som är större än EOF, och uppspelningen startar från början med MSE.</p> <p>・ 19049: Inget feltillstånd rapporterades för Flash Player i Chrome, IE och Firefox när video blockeras under uppspelningen.</p> <p>・ 17205: Videouppspelningen avbryts vid uppspelning av omultiplicerad ström under några timmar medan ljudet fortsätter att spelas upp (Chromium-nummer 664033).</p> <p>・ 12308: DASH-strömmar med composition_time_offset angiven kan ha TimeStampOffset tillämpat på den i Chrome-webbläsaren, vilket kan leda till negativ avkodningstid och därmed ett fel som stöds av MEDIA_ERR_SRC_NOT_ (Chromium issue #398141).</p> <p>・ 14126: Uppspelningen kan avbrytas i Firefox (utgåva 1316024) på grund av den interna luckan i MSE-källbufferten. Försök att söka för att återuppta uppspelningen.</p> <p>・ 19115: MS Edge och IE 11 (Win 8.1 och 10) anger inte Origin till null vid CORS-omdirigering och misslyckas ändå eftersom huvudet inte är null vilket leder till uppspelningsfel.</p> <p>・ 19861: Problem med att lägga till beteende i källbuffert för media som redan spelats upp. Chrome avvisar det tillagda fragmentet inklusive moov, vilket orsakar efterföljande avkodningsfel. (Krom nr 735335)</p> <p>19921: Uppspelning stoppas för visst HLS-innehåll trots att det har buffrats (Chromium-utgåva nr 713540)</p> <p>・ 20444:Om du söker till slutet av buffertintervallet på IE och Edge kan uppspelningen stoppas.</p> <p>・ 20511: Ibland kan avvisning observeras för HLS-strömmar med eller utan annonser.</p> <p>・ 20743: I Windows 10 Chrome spelas HLS Live-strömmen upp några sekunder innan MP4-uppspelningen spelas upp.</p> <p>・ 21043: Det är inte säkert att videodimensionen är korrekt vid den första inläsningen på grund av brist på metadata.</p> <p>・ 21115: Android-användargest krävs för att starta uppspelningen om förhandsgranskningsannons är tillgänglig för videor i en spellista.</p> <p>・ HLS Live har inte stöd för tidsstämpelrollover.</p> <p>・ AAC-SSR-ljud stöds inte.</p> <p>Ljudkodekar AC3 och Enhanced AC3 stöds inte.</p> <p>・ För strömmar med tidsstämpelavbrott men utan kontinuitetsmarkörer</p> <p>・ Uppspelning kan ha problem och felaktig sökning på grund av hopp.</p> <p>・ Innehållets längd och uppspelningstiden kanske inte stämmer överens.</p> <p>・ Ojämnheter mellan representationer och renderingar bör överensstämma med andra metoder kan leda till problem med synkronisering och kvarvarande.</p> <p>・ Bildtexter och WebVTT kanske inte visas i närheten av strömmens slut.</p> <p>・ Ändringar i ljudkodeken stöds inte vid tidsstämpelhopp.</p> <p>・ Annonsinfogning stöds inte.</p> <p>・ Snabbläge framåt kan leda till uppspelningsloop på Win 8.1 IE 11 (MS-problem 12446268).</p> <p>DASH:</p> <p>・ För liveströmmar stöds liveprofiler med dynamisk typ.</p> <p>・ För VoD-strömmar stöds live-profiler med statisk typ.</p> <p>För VoD-strömmar är ondemand-profilen inte certifierad för annonsarbetsflöden.</p> </td> 
   <td><p>・ DASH Live- och DASH Video on Demand-strömmar stöds inte.</p> <p>・ PIP-videouppspelning (Picture in Picture) stöds inte i helskärmsläge i iOS.</p> <p>I Safari-tillägget (Video Tag) fungerar inte mindre manifest utan rätt innehållstyphuvud.</p> </td> 
   <td><p>・ applicationID i avsändarappen måste vara detsamma som genereras när mottagarens URL registreras som en anpassad mottagarapp.</p> <p>・ Referensspelaren är certifierad för DASH-arbetsflöden. Gränssnittsramverket är inte certifierat.</p> <p>En lista över mediekodekar som stöds finns i <a href="https://developers.google.com/cast/docs/media"><em>här</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>Allmän uppspelning (Spela upp, Pausa, Sök)</td> 
   <td> </td> 
   <td>18098: Vissa sökproblem har observerats med HLS LBA FER-ström.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Adaptiv bithastighet</td> 
   <td><p>・ 20079: Buffer re-write on seek within buffer range.</p> <p>2008: Flashens ABR-beteende överensstämmer med MSE.</p> </td> 
   <td><p>・ Reservvarianten för endast ljud i en ABR-ström ignoreras på grund av buffertrelaterade begränsningar.</p> <p>・ 12289: ABR-kontrollparametrar gäller inte för ljud vid HLS-/DASH-strömmar utan multiplikation.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>608/708 Bildtexter</td> 
   <td> </td> 
   <td><p>・ 7810: I Android 4.4.4 verkar Chrome inte ha stöd för grundläggande CSS-teckensnittsfamiljer som används av spelaren, vilket innebär att funktionen för teckensnittsändring inte fungerar.</p> <p>・ CC-kanalerna kan inte ändras för 608 bildtexter.</p> <p>・ Avancerade formateringsfunktioner stöds inte för 608 bildtexter.</p> <p>Inbäddade bildtexter (608/708) som signaleras via taggen Accessibility stöds.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>・ 5206: Regiontaggar i WebVTT-filen ignoreras av spelaren när bildtexterna visas.</p> <p>・ DASH: Fragmenterade/segmenterade VTT-filer stöds inte.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Manifestredundans</td> 
   <td>21056: Med Flash Fallback sker inte failover för Live-strömmen om den primära strömmen returnerar ett 404-fel under uppspelningen.</td> 
   <td>Manifestväxling kan bara användas för innehåll och inte för annonser.</td> 
   <td>Missing playlist failover works on Safari only for HTTP error code 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Avancerad redundans</td> 
   <td> </td> 
   <td><p>・ Segmentredundans stöder inte att otillgängliga segment hoppas över och uppspelningen fortsätter.</p> <p>20533: Segment som saknas i en spellista ska behandlas som Kontinuitet och uppspelningen bör återupptas från nästa tillgängliga segment.</p> <p>21267: Strömväxling på grund av failover kan leda till hämtning av äldre segment.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>QoS- och Player-meddelanden</td> 
   <td>21129: Bildrutefrekvensen är inte tillgänglig vid återgång av Flash.</td> 
   <td><p>• 11170:</p> <p>Timed_Event är inte tillgängligt för webbläsarens TVSDK med MSE, till skillnad från webbläsarens TVSDK med Flash Fallback.</p> <p>21129: Bildrutefrekvensen beräknas inte för liveströmmar.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Stöd för Cookie-rubriker</td> 
   <td> </td> 
   <td> </td> 
   <td><p>Flaggan withCredentials och cookie-rubriker stöds inte i Safari.</p> <p>21051: Om du vill tillåta cookies i Safari aktiverar du inställningen "Cookies and website data" (Cookies och webbplatsdata) i Inställningar &gt; Sekretess.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Egna taggar</td> 
   <td>14763: Anpassade taggar som inte börjar med # bör inte stödjas. Just nu skapas TimedMetadata-objektet och rapporteras för sådana taggar under Flashen Fallback.</td> 
   <td>Strömmar med anpassade interna taggar är inte certifierade.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Ljud för sen bindning</td> 
   <td> </td> 
   <td><p>・ Ad-infogning stöds inte med HLS Live LBA-strömmar.</p> <p>・ 17273: HLS VOD LBA-strömmar växlar till standardåtergivning vid växling vid fel och kan inte växlas tillbaka till den senast valda.</p> <p>・ 20251: HLS Live LBA-strömmen kan avbrytas vid sökning.</p> <p>・ 20497: Spelaren är fortfarande i buffertläge om HLS LBA unmuxed-strömmar saknar ljud- eller videobildrutor nära slutet av strömmen.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>302 Omdirigering</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>omdirigeringsoptimering stöds inte i Windows Edge- och IE-webbläsare eftersom dessa inte stöder egenskapen responseURL i XMLHttpRequest-objektet.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 17: Avancerade uppspelningsfunktioner**

<table> 
 <tbody> 
  <tr> 
   <td>Innehållstyp</td> 
   <td>Funktion</td> 
   <td>Flash</td> 
   <td><strong>HTML 5 i Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 i Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (endast DASH-uppspelning)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Uppspelning vid förskjutning</td> 
   <td><p>Det går inte att starta uppspelning med ett visst förskjutningsvärde för MP4-innehåll.</p> </td> 
   <td>20492: Annonser i mellanrullar före förskjutningen spelas upp innan innehållet återupptas från förskjutningsvärdet.</td> 
   <td>Uppspelning med förskjutningsfunktion stöds inte i iOS.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Trick Play</td> 
   <td>Smooth Trickplay fungerar inte för strömmar som saknar iFrame-renderingar.</td> 
   <td><p>・ Trick Play-anpassningar stöds inte i Firefox och Internet Explorer och det omvända trickläget är därför inte tillgängligt i dessa webbläsare.</p> <p>・ Trickplay är inte tillgängligt när innehåll spelas tillsammans med annonser.</p> <p>・ 10435: Under DASH-uppspelning låser sig videon vid framåtriktad tricks i Internet Explorer (Win 8.1)</p> <p>ibland. Detta sker eftersom vi använder videoelementen playbackRate utan tricket play-anpassning.</p> <p>14182: Vid tillbakaspolning i webbläsaren Chrome kanske inte seek-händelsen tas emot och trickläget fungerar därför inte.</p> <p>・ 14942: Uppspelningshastigheten kan ställas in för Chrome för Android även om uppspelningen inte är tricks, men inställningen används inte och uppspelningen fortsätter med normal hastighet.</p> <p>・ 17308: Sökning fungerar inte i trickläge.</p> <p>・ 17309: I webbläsaren Chrome går det inte att använda det omvända tricket i mer än 2 sekunder.</p> <p>19272: Trickuppspelningen kanske inte återställs efter buffring i webbläsaren Windows 10 Edge om det finns DASH-strömmar.</p> </td> 
   <td>Det finns inte stöd för läget Spola tillbaka.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>ID3-parsning</td> 
   <td>20346: Textkodningsbyte för ID3-bildrutor ska också returneras av SDK.</td> 
   <td><p>ID3-taggar som finns i ADTS (Audio Data Transport Streams) ignoreras av SDK.</p> <p>・ 12378: Tidsbestämda ID3-metadata tolkas vid olika tidpunkter på Flash och i webbläsare med stöd för MSE, vilket innebär att visningsbeteendet på tidslinjen i referensspelaren också är annorlunda.</p> <p>・ 19247: ID3-parsning stöds inte i gränssnittsramverket.</p> </td> 
   <td><p>・ 20323: PRIV ID3-tagg som används för att signalera tidsstämpeln för det första urvalet av varje segment tolkas inte av Safari (Safari-problem nr 32422733)</p> <p>・ 20350: På vissa enheter (inklusive MAC OS X 10.1, iPad10) tillhandahåller Safari inte en händelse för cue change när i trickläge, vilket innebär att ID3-bildrutor inte tas emot. (Safari-nummer 32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Stöd för brytpunkter</td> 
   <td> </td> 
   <td><p>・ Annonsinfogning på klientsidan stöds inte med HLS-strömmar som innehåller avbrott.</p> <p>・ Ljudkodekändring tillåts inte för avbrott i HLS-strömmen.</p> <p>・ Ljudspårsomkopplaren stöds inte för HLS-strömmen med brytningsmarkörer</p> </td> 
   <td>Sekvensnummer för avbrott är ett krav för HLS-strömmar med avbrott för uppspelning på Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 18: Innehållsskyddsfunktioner**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Innehållstyp</strong></td> 
   <td><strong>Funktion</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML 5 i Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 i Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (endast DASH-uppspelning)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>Byteintervallet stöds inte med AES-128-krypterat innehåll.</td> 
   <td>12324: HLS AES-128-krypterade strömmar kan inte spelas upp i Safari om IV-taggen inte anges.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>・ 12660: HTML5-spelaren returnerar ett internt serverfel för PlayReady-krypterat streckinnehåll som har gått ut.</p> <p>・ 16720: DASH DRM-krypterat innehåll fungerar inte om startattribut i punkttagg saknas.</p> <p>・ 18589: Uppspelning stöds inte för DRM-skyddade Dash VoD Multiperiod-strömmar med Xlink.</p> <p>・ 18653: Uppspelning av brett MultiPeriod-innehåll med flera tangenter, stoppas vid första perioden och kan inte växla till nästa period.</p> <p>・ 18656: MultiPeriod Stream för uppspelning, krypterad med olika nycklar, spelar inte upp.</p> <p>Playready 2.0 for Dash är inte certifierat.</p> <p> </p> <p> </p> </td> 
   <td>12602: HLS Fairplay DRM-metadata uppdateras upprepade gånger av HTML5-spelaren i Safari</td> 
   <td><p>DASH WideVM-innehåll som paketeras via Bento4 kan spelas upp. Innehåll som paketerats via Offline Packager och Shaka Packager kan inte spelas upp. DASH PlayReady DRM stöds inte.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 19: Core Ad Insertion Features (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Innehållstyp</strong></td> 
   <td><strong>Funktion</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML 5 i Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 i Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (endast DASH-uppspelning)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Före/Mid/Post</td> 
   <td> </td> 
   <td><p>・ Inledande annonser med HLS-innehåll spelas upp i läget Dubbla spelare.</p> <p>・ DASH-annonser med HLS-innehåll och HLS-annonser med DASH-innehåll stöds inte.</p> <p>・ 19002: I HTML5 Player med MSE och Break. insertionType returnerar inte rätt värde för att visa rätt infogningstyp, d.v.s. klienten infogad och/eller servern infogad.</p> <p>7794: På mobila enheter (iOS, Android med Chrome 33 eller senare eller inbyggd webbläsare) där standardkontrollfältet visas i helskärmsläge, är sökfältet och snabbspolarna tillgängliga när annonsuppspelning används.</p> <p>・ 11048: Det går inte att växla från annons till HLS Live-innehåll på ett smidigt sätt när det gäller tillägg för mediekälla.</p> <p>・ 16083: På Android 4.4 Chrome v52 kan HLS och HLS-innehåll ibland leda till avkodningsfel i pipeline efter uppspelningen har avinstallerats.</p> <p>・ 16097: Fel som inträffar under Ad break hanteras inte, vilket kan göra att huvudströmmen avbryter uppspelningen.</p> <p>・ 18095: MP4-annonser stöds inte med HLS-direktinnehåll.</p> <p>19120: Flera sökningar på HLS-annonser med HLS-innehåll kan göra att strömmen avbryter uppspelningen.</p> <p>・ 19131: Buffrande övertäckning kan uppträda när man växlar från pre-roll och break till content.</p> <p>・ 20296: När det gäller HLS Live-strömmar kan uppspelningen stoppas om du söker tillbaka i DVR-fönstret följt av att söka efter över matchade mittrullar.</p> <p>・ 20298: HLS Live-strömmar med mittrullar stannar det ögonblick då den första mittrullen flyttas ut ur DVR-fönstret.</p> <p>・ 20317: HLS Live-strömmar kan hänga sig vid växling till nästa annons eller från annons till innehåll om radbrytningar innehåller mer än en annons.</p> 
    <ul> 
     <li>Ads in the DVR window of HLS Live streams are not resolved.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK respekterar inte sekvensattribut i VMAP-svar för VAST och Source.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: SDK respekterar inte sekvensattributet i VMAP-svaret för VAST och Source.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: Attributet VMAP repeat stöds inte.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Creative Repackaging</td> 
   <td> </td> 
   <td>21464: Annonssvaret ignoreras helt om den kreativa ompackningen misslyckas för en av annonserna i reklambrytningen.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 20: Avancerade funktioner för Ad Insertion (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Innehållstyp</strong></td> 
   <td><strong>Funktion</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML 5 i Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML 5 i Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (endast DASH-uppspelning)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Endast annons</td> 
   <td> </td> 
   <td>20056: Egenskapen Player-teknik är inte relevant eftersom den baseras på huvudinnehållet, som är tomt vid uppspelning med endast annons</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Anpassad annonspolicy</td> 
   <td> </td> 
   <td><p>・ Annonsbeteenden stöds inte med MP4-annonser och MP4-innehåll.</p> <p>・ 13973: Anpassade annonsinställningar - SKIP-principen genererar inte complete-händelse när den används med MSE.</p> <p>・ 14939: Anpassade annonseringsbeteendeprinciper fungerar inte för DASH-innehåll.</p> <p>・ 17131: Den första bildrutan i annonsen visas och sedan återupptas innehållet om man vill ha en HOS SKIP- och break-policy.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Pressmeddelanden/bannerannonser/Klickbara annonser</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Banderollannonser visas inte när referensspelaren används.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>・ Annonsbeteenden stöds inte för VPAID-annonser.</p> <p>・ 15032: VPAID-annonser i kombination med MP4- eller HLS-annonser i en annonsbrytning stöds inte.</p> <p>・ 19001: På Android och iOS kan dubbla ljudspår höras när VPAID-annonser spelas upp med MP4 som huvudinnehåll, ett av huvudinnehållet och en av annonserna.</p> <p>・ 20762: VPAID-annonser stöds inte med PIP (Picture in Picture).</p> <p>・ 21172: Händelsen Play complete tas inte emot för HLS VOD-innehåll med VPAID-annonser.</p> <p>・ 21173: onAdBreakCompleteEvent tas inte emot för HLS VOD-innehåll och post roll VPAID-annonser.</p> </td> 
   <td>Spelaren växlar mellan normalläge och helskärmsläge när du växlar mellan VPAID och huvudinnehåll.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabell 21: Integreringar**

| **Innehållstyp** | **Funktion** | **Flash** | **HTML 5 i Firefox, IE, Chrome, Android Chrome** | **HTML 5 i Safari, iOS Safari** | **Chromecast (endast DASH-uppspelning)** |
|---|---|---|---|---|---|
| VOD + Live | Integrering med Adobe Analytics VHL |  | 19004: Spårning av videoanalyser är inte tillgängligt via verktyget för gränssnittskonfigurator. |  |  |

## Användbara resurser {#helpful-resources}

* Se den fullständiga hjälpdokumentationen på [Adobe Primetime Läs mer &amp; Support](https://experienceleague.adobe.com/docs/primetime.html) sida.
