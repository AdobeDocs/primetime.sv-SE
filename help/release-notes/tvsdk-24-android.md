---
title: Versionsinformation om TVSDK 2.4.1 för Android
description: Versionsinformation om TVSDK 2.4.1 för Android beskriver de nya och stödda funktionerna och de kända problemen och begränsningarna i TVSDK Android 2.4.1.
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 3de09048-ae32-43b4-a019-34b217931a4c
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Versionsinformation om TVSDK 2.4.1 för Android {#tvsdk-for-android-release-notes}

Versionsinformation om TVSDK 2.4.1 för Android beskriver de nya och stödda funktionerna och de kända problemen och begränsningarna i TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe släpper TVSDK 2.4.1 för Android.

Om du vill använda den här versionen av TVSDK måste du kontrollera att datorn uppfyller de krav som beskrivs i [Systemkrav](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

Här hittar du dokumentation:

・ Onlinehjälpsystemet TVSDK 2.4 för Android-hjälp

・ [Javadocs TVSDK 2.4 för Android Java API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadocs är den ultimata auktoriteten eftersom de automatiskt genereras direkt från TVSDK-källkoden.

・ [API-dokumentation för C++ för TVSDK 2.4 för Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Varje Java-klass har en motsvarande C++-klass, och C++-dokumentationen innehåller mer förklarande material än Javadocs, så se C++-dokumentationen för en mer detaljerad förståelse av Java API.

・ Migreringsguide ([Migreringshandbok för TVSDK 2.4 för Android](../migration-guides/tvsdk-14-25-android.md))

I den här guiden förklaras vad du behöver ändra för att migrera ett program baserat på TVSDK 1.4 till ett som baseras på TVSDK 2.4.

## Nya funktioner {#new-features}

TVSDK 2.4.1 för Android ger många prestandaförbättringar jämfört med tidigare versioner. Det ger en högkvalitativ tittarupplevelse.

Den här versionen innehåller alla funktioner i version 2.4 och 2.4.1 och inga funktioner är föråldrade.

Här är de viktigaste nya funktionerna i version 2.4.1:

* Funktioner i HLS version 4

   * **Videouppspelning** (spela upp, pausa, söka) med spelarkontroll för live-, linear- och VOD-strömmar.
   * **Undertexter.** TVSDK kan visa undertexter för 608/708 med ett urval av teckensnitt, teckenstorlekar, färger och bakgrund. Det kan även stödja videor med uppslagna beskrivningar och växla mellan språkspår om sådana finns.
   * **Trick play mode** har stöd för snabb framåtspolning och tillbakaspolning för HLS-strömmar som använder I-Frames. Alla videouppspelningskontroller fungerar på innehållet. Långsam rörelse (framåt) är tillgängligt för externt videouppspelningsläge med hastigheter mellan 0 och 1.
   * **Adaptiv bithastighet (ABR)** låter spelaren dynamiskt välja vilken av flera versioner av samma innehållsström som ska spelas upp, baserat på nätverk och andra förhållanden. Du kan ange parametrar dynamiskt eller i manifestfilen för att välja bland aggressiva, måttliga och konservativa markeringsprinciper.
   * **Byteintervall** kan en enda TS-fil innehålla flera TS-segment.
   * **Alternativa ljudåtergivningar** gör att spelaren kan växla mellan tillgängliga ljudspår.
   * **ID3-stöd.** TVSDK kan spela upp HLS-ljud- och videoströmmar som innehåller ID3-ljudmetadata, till exempel artistnamn, titel och album.
   * **Redundans. **TVSDK använder strategier för att fortsätta oavbruten uppspelning, trots fel i värdservrar, spellistfiler och segment.
   * **Flerkanaligt ljudpass-through (DD+).** TVSDK kan skicka Dolby Digital Plus-ljuddata (E-AC3) till hårdvara.

* Innehållsskyddsfunktioner

   * **DRM för HLS.** Alla API:er för videouppspelning fungerar med krypterat videomaterial som skyddas av Adobe Access. Följande DRM-funktioner stöds:

      * Licensrotation
      * Nyckelrotation
      * Licenscachning
      * Principtid
      * IV-rotation

* **AES 128-uppspelning.** TVSDK kan spela upp HLS-innehåll enligt den avancerade krypteringsstandarden (AES) med en nyckelstorlek på 128 bitar.
* **Skyddad HLS (PHLS)** innehåller en begränsad uppsättning färdiga DRM-principer, en deluppsättning av vad Adobe Access erbjuder, för att aktivera lättviktig DRM över HLS för live- och VOD-strömmar.

* Reklam/alternativt innehåll och intäktsfunktioner

   * **Spårning för annonser som infogats på serversidan.** TVSDK kan spåra annonser som infogats av annonsinfogningstjänsten i Adobe Cloud. Det har stöd för linjära annonser i formaten VAST2, VAST3 och VMAP för VOD och live/linear streams.
   * **Anpassade HLS-taggar.** TVSDK använder `MediaPlayerConfig` för att aktivera meddelande till spelarprogrammet när anpassade HLS-taggar visas i strömmen.
   * **Annonsinfogning på klientsidan.** Biblioteket för annonsinfogning i Auditude fungerar tillsammans med Adobe Auditude-servrar för att matcha annonser för dynamisk infogning i live-, linjärt- och VOD-innehåll, både före- och efter-rollpositioner.
   * **Anpassade annonslösare.** The `ContentResolver, OpportunityGenerator,` och `MediaPlayerClientFactory` Med -gränssnitt kan du implementera en anpassad annons/alternativ innehållshanterare och registrera en anpassad affärsmöjlighetsdetektor för att arbeta med TVSDK. The `TestAdResolver` och `AuditudeResolver` -klasser innehåller C++-exempel på implementering av en innehållslösare. Du hittar ett Javascript-exempel på `samples/jspsdk/testapp/psdk.js`.
   * **Enhetligt annonsbeteende.** Använd `AdPolicySelector` -gränssnitt för att aktivera konsekvent beteende för alla spelare för åtgärder som sökning och tricks spelar när det finns annonser i innehållet. Om du inte implementerar din egen, använder TVSDK `DefaultAdPolicySelector`.
   * **Ta bort/byt ut C3-annonser.** Använd lämpligt TVSDK API för att ta bort anpassade innehållsområden och dynamiskt infoga nya annonser utan ytterligare förberedelser. Detta är praktiskt när live/linjärt innehåll sänds och sedan omedelbart görs tillgängligt på begäran utan rensning.

Här är de viktigaste nya funktionerna i version 2.4:

* **Direkt aktiverad för VOD och live** När du aktiverar direkt, initierar och buffrar TVSDK media innan uppspelningen startar. Eftersom du kan starta flera `MediaPlayerItemLoader` -instanser samtidigt i bakgrunden kan du buffra flera strömmar. När en användare ändrar kanalen och strömmen har buffrats korrekt startar uppspelningen på den nya kanalen omedelbart. TVSDK 2.4 har även stöd för Instant On för liveströmmar. De aktiva strömmarna buffras om när det aktiva fönstret flyttas.

* **Prestandaförbättringar **Den nya TVSDK 2.4-arkitekturen har flera prestandaförbättringar:

   * **Delsegmentering** - TVSDK minskar ytterligare storleken på varje fragment för att starta uppspelningen så snart som möjligt.
   * **Parallella annonshämtningar** - TVSDK förhämtar annonser parallellt med innehållsuppspelningen innan annonsuppspelningen avbryts, vilket möjliggör smidig uppspelning av annonser och innehåll.
   * **Lazy-annonsupplösning** - Med den här funktionen väntar vi inte på att icke-preflight-annonser ska matchas innan uppspelningen startar, vilket minskar starttiden. API:er som sökning och uppspelning är fortfarande inte tillåtna förrän alla annonser är lösta.

* **Uppspelning av MP4-innehåll**

Den här versionen av TVSDK stöder uppspelning av MP4 som huvudinnehåll.

* **Beständiga nätverksanslutningar**

TVSDK upprätthåller en uppsättning återanvändbara nätverksanslutningar, så det medför inte någon belastning för att skapa och förstöra en nätverksanslutning för varje nätverksbegäran.

* **Upplösningsbaserat utdataskydd**

Den här funktionen kopplar uppspelningsbegränsningar till specifika upplösningar och ger mer detaljerade DRM-kontroller.

* **Trick play med adaptiv bithastighet (ABR)**

Med den här funktionen kan TVSDK växla mellan iFrame-strömmar i trickuppspelningsläge. Du kan använda profiler som inte är iFrame-profiler för att trigga uppspelningen med lägre hastigheter.

* **Smidigare tricks**

De här förbättringarna förbättrar användarupplevelsen:

・ Anpassad bithastighet och bildrutehastighet vid uppspelning, baserat på bandbredd och buffertprofil

・ Använd huvudströmmen i stället för IDR-strömmen för att få upp till 30 fps snabb uppspelning.

* **Förbättrad ABR-logik**

Den nya ABR-logiken baseras på buffertlängd, förändringshastighet för buffertlängd och uppmätt bandbredd. Detta garanterar att ABR väljer rätt bithastighet när bandbredden ändras och även optimerar antalet gånger som bithastighetsväxlingen faktiskt sker genom att övervaka den hastighet med vilken buffertlängden ändras.

* **Fakturering**

TVSDK samlar automatiskt in mätvärden och följer kundförsäljningskontraktet för att generera periodiska användningsrapporter som krävs för faktureringsändamål. I varje direktuppspelningshändelse använder TVSDK Adobe Analytics API för att skicka faktureringsmått som innehållstyp, aktiverade markeringar för annonsinfogning och DRM-aktiverade flaggor - baserat på den fakturerbara strömmens varaktighet - till den rapportserie som ägs av Adobe Analytics Primetime. Detta stör inte och ingår inte i kundens egna Adobe Analytics-rapporteringsprogram eller serversamtal. På begäran skickas den här användningsrapporten regelbundet till kunderna. Detta är den första fasen av faktureringsfunktionen som endast stöder fakturering av användning. Den kan konfigureras baserat på försäljningskontraktet med hjälp av de API:er som beskrivs i dokumentationen.

## Funktioner som stöds {#supported-features}

TVSDK för Android 2.4 har stöd för ett antal funktioner som du kan implementera för att lägga till funktioner i dina videoprogram.

>[!NOTE]
>
>I funktionens matristabeller nedan betyder en Ö att funktionen stöds i den aktuella versionen.

### Kärnfunktioner för uppspelning {#core-playback-features}

| **Funktion** | **Innehållstyp** | **HLS** | **DASH** |
|---|---|---|---|
| Allmän uppspelning (Play, Pause, Seek) | VOD + Live | Ð | ² (endast VOD) |
| FER - Allmän uppspelning (Play, Pause, Seek) | FER VOD | Ð | Stöds inte |
| MP3 | VOD | Stöds inte | Stöds inte |
| Uppspelning av MP4-innehåll | VOD | Ð | Ð |
| Adaptiv logik för växling av bithastighet | VOD + Live | Ð | Stöds inte |
| Uppspelning endast av ljud | VOD + Live | Ð | Stöds inte |
| Undertexter - 608/708 | VOD + Live | Ð | ² (endast VOD) |
| Undertexter - WebVTT | VOD + Live | Ð | ² (endast VOD) |
| Manifestväxling vid fel | VOD + Live | Ð | ² (endast VOD) |
| Avancerad redundans | VOD + Live | Ð | ² (endast VOD) |
| QoS och spelarmeddelanden | VOD + Live | Ð | ² (endast VOD) |
| Stöd för cookie-rubriker | VOD + Live | Ð | ² (endast VOD) |
| Stöd för anpassade rubriker | VOD + Live | Stöds inte | Stöds inte |
| Ange parametrar för buffertkontroll | VOD + Live | Ð | ² (endast VOD) |
| Ange adaptiva bithastighetskontroller | VOD + Live | Ð | ² (endast VOD) |
| Anpassade Manifest-taggar (HLS)/händelseströmmar (DASH) | VOD + Live | Ð | ² (endast VOD) |
| Sena bundna ljud | VOD + Live | Ð | ² (endast VOD) |
| 302 Omdirigering | VOD + Live | Ð | ² (endast VOD) |

### Avancerade uppspelningsfunktioner {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>Funktion</strong></td> 
   <td><strong>Innehållstyp</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Uppspelning med förskjutning</td> 
   <td>Live</td> 
   <td>Ð</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Uppspelning endast av ljud</td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Trick Play </td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Smooth Trick Play (med ABR)</td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>ID3-parsning (HLS) / Timed Metadata (DASH)</td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Utpressningar </td> 
   <td>VOD + Live</td> 
   <td>Stöds inte</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Direkt på</td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Stöd för brytpunkter (HLS) </li> 
     <li>Flera punkter (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>302 Omdirigera Stickyness</td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>² (endast VOD)</td> 
  </tr>
  <tr>
   <td>Skrubbning av miniatyrbilder (iFrame och JPEG)</td> 
   <td>VOD + Live</td> 
   <td>Stöds inte</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Strömintegritet </td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>Stöds inte</td> 
  </tr>
 </tbody>
</table>

### Core Ad Insertion Features (CSAI) {#core-ad-insertion-features-csai}

| **Funktion** | **Innehållstyp** | **HLS** | **DASH** |
|---|---|---|---|
| Allmän uppspelning, annonser aktiverade | VOD + Live | Ð | ² (endast VOD-förrullningar) |
| FER-innehåll med annonser aktiverade | VOD | Ð | Stöds inte |
| Standardbeteenden för annonser | VOD + Live | Ð | ² (endast VOD-förrullningar) |
| VAST 2.0/3.0 | VOD + Live | Ð | ² (endast VOD-förrullningar) |
| VMAP 1.0 | VOD + Live | Ð | ² (endast VOD-förrullningar) |
| MP4-annonser | VOD + Live | ² (från CRS) | ■ (från CRS, endast för rullning) |

### Advanced Ad Insertion Features (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Funktion</strong></td> 
   <td><strong>Innehållstyp</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Trick Play med annonser aktiverade</td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Endast annons </td> 
   <td>VOD</td> 
   <td>Stöds inte</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Målparametrar</td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>² (endast VOD-förrullningar)</td> 
  </tr>
  <tr>
   <td>Egna parametrar</td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>² (endast VOD-förrullningar)</td> 
  </tr>
  <tr>
   <td>Anpassade annonsbeteenden</td> 
   <td>VOD + Live</td> 
   <td>Ð</td> 
   <td>² (endast VOD-förrullningar)</td> 
  </tr>
  <tr>
   <td>Anpassade annonstaggar</td> 
   <td>Live</td> 
   <td>Ð </td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Anpassade annonslösare</td> 
   <td>VOD + Live</td> 
   <td>Ð </td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Anpassad annonslösning för frihjulshjul</td> 
   <td>VOD</td> 
   <td>Stöds inte</td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>C3 Ad Replacement </td> 
   <td>VOD + Live</td> 
   <td>Ð </td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Lazy Ad Loading</td> 
   <td>VOD</td> 
   <td>Ð </td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Stöd för brytpunkter - SSAI (HLS) </li> 
     <li>Flera punkter (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>Ð </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Companion Ads, Banner Ads och Clickable Ads</td> 
   <td>VOD + Live</td> 
   <td>Ð </td> 
   <td>² (endast VOD-förrullningar)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Live</td> 
   <td>² (JS) </td> 
   <td>² (endast VOD-förrullningar)</td> 
  </tr>
  <tr>
   <td>Tidigt annonsutträde</td> 
   <td>Live</td> 
   <td>Ð </td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>Regelbaserad Creative VOD + Live Prioritization</td> 
   <td>VOD + Live</td> 
   <td>Ð </td> 
   <td>Stöds inte</td> 
  </tr>
  <tr>
   <td>CRS-regler </td> 
   <td>VOD + Live</td> 
   <td>Ð </td> 
   <td>Stöds inte</td> 
  </tr>
 </tbody>
</table>

## Funktioner för innehållsskydd {#content-protection-features}

| **Funktion** | **Innehållstyp** | **HLS** | **DASH** |
|---|---|---|---|
| AES-kryptering | VOD + Live | Ð | ² (endast VOD) |
| AES-kryptering - exempel | VOD + Live | Ð |  |
| Tokeniserade strömmar | VOD + Live | Ð |  |
| DRM | VOD + Live | Primetime DRM only (Future: WideVM) | Endast bredbara |
| Extern uppspelning (RBOP) | VOD + Live | Endast Primetime DRM | Stöds inte |
| Licensrotation | VOD + Live | Endast Primetime DRM | Stöds inte |
| Nyckelrotation | VOD + Live | Endast Primetime DRM | Stöds inte |

### Integreringsfunktioner {#integration-features}

| **Funktion** | **Innehållstyp** | **HLS** | **DASH** |
|---|---|---|---|
| Integrering med Adobe Analytics VHL | VOD + Live | Ð | Ð |
| Fakturering | VOD + Live | Ð | Stöds inte |

## Funktioner som inte stöds {#features-not-supported}

Den här versionen av TVSDK stöder inte:

* Utpressning av annonser.
* Långsam rörelse i tricks.
* Söka och tricka med MP4-innehåll.
* Lägg in med huvudinnehållet i MP4.
* Sök efter när en annons spelas.
* Uppspelning av annonser med media som bara innehåller ljud.

## Kända fel och begränsningar {#known-issues-and-limitations}

Den här versionen av TVSDK har följande problem:

* Enhetsspecifik (Samsung Galaxy Tab 4) kraschar VOD DRM LBA med ljud och klicka på annonser
* Annonsen spelas inte upp för ett visst innehåll.
* Det går inte att ange bildtexten close till CJK-språk.
* Videon kan komma ut ur trickläget automatiskt mellan både VOD och live.
* VHL - fel hjärtslagsanrop skickas när vi startar ett innehåll från en förskjutning.
* När VPAID-annonser spelas upp anrop till VHL-pulsslag för händelse:type:play-annons saknas.
* Annonser i förväg spelas upp även när adBreakPolicy SKIP har valts.
* När du har startat en Complete-lägesspelare återgår du till uppspelningsläget med SKIP adBreakPolicy för postrollannonser.

Utan video finns det ingen visningsrutedimension och utan visningsrutedimension kan du inte visa grafik för bildtexter.

## Användbara resurser {#helpful-resources}

* Se den fullständiga hjälpdokumentationen på [Adobe Primetime Läs mer &amp; Support](https://experienceleague.adobe.com/docs/primetime.html) sida.
