---
title: Versionsinformation om TVSDK 1.4 för Desktop HLS
description: Versionsinformationen för TVSDK for Desktop HLS beskriver vad som är nytt eller ändrat, de lösta och kända problemen i TVSDK DHLS.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5196'
ht-degree: 0%

---


# Versionsinformation om TVSDK 1.4 för Desktop HLS {#tvsdk-for-desktop-hls-release-notes}

Versionsinformationen för TVSDK for Desktop HLS beskriver vad som är nytt eller ändrat, vad som är löst och vad som är känt i TVSDK DHLS.

## Nya funktioner {#new-features}

**1.4.31**

* **Multi-CDN-stöd för CRS-annonser**

   * Som standard lagras alla omkodade resurser på ett CDN som ägs av Adobe på Akamai. Med den senaste versionen kan Adobe Creative Repackaging Service (CRS) överföra de trancoded creatives till flera CDN:er enligt kundens specifikationer.
   * Nya API:er läggs till i TVSDK för att göra det möjligt att ange den slutliga kreativa URL:en för CRS när standard-URL:en inte används. Läs dokumentationen för att lära dig hur du använder dessa nya API:er.

### Nya funktioner i tidigare versioner {#new-features-previous}

**1.4.30**

* **Faktureringsstatistik**

För att passa kunder som bara vill betala för det de använder, i stället för en fast avgift oavsett faktisk användning, samlar Adobe in användningsuppgifter och använder dessa värden för att avgöra hur mycket kunderna ska faktureras.

**1.4.24**

* **Beständig nätverksanslutning**

Viktigt: Du måste ha minst Adobe Flash Player version 22 eller senare installerad.
Beständiga nätverksanslutningar skapar och lagrar en intern lista över nätverksanslutningar som kan återanvändas för flera begäranden i stället för att öppna en ny anslutning för varje nätverksbegäran. Beständiga nätverksanslutningar bör öka effektiviteten och minska latensen i nätverkskoden.

I den här versionen stöds inte den här funktionen i Apple Safari och Mozilla Firefox på Mac.

**1.4.19**

* Stöd för strömintegritet för VPAID-annonser.
* Aktiverade tabbalternativet tyst i Flash Player FP 20.0.0.267 för Firefox 42 och senare genom att åtgärda problemet med hängning.

**1.4.18**

* Primetime Desktop HLS TVSDK har nu stöd för VPAID 2.0 Linear SWF-kreatörer för en interaktiv annonsupplevelse i strömmen.

**1.4.10**

* **Ad Fallback, Daisy chaining in ad ad selection logic (Zendesk #3103)** For VAST ads (creatives) with the fallback rule enabled, the TVSDK behandlar en annons med en ogiltig MIME-typ som en tom annons och försöker använda reservannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.

Mer information finns i [Lägg till reservversioner för VAST- och VMAP-annonser](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **Video Heartbeats Library (VHL) uppdaterad till version 1.5**

   * Möjlighet att skicka metadata med videostart och/eller video-/annons-/kapitelstart som kontextdata
   * Mindre nätverkstrafik - antalet pulsslag är i genomsnitt mindre och mindre.

**1.4.7**

* **Individuellt stöd**

Stöd för lokala installationer av Adobe Individualization Server för att anpassa klientens individualiseringsbegäran och gå till en annan slutpunkt.

**1.4.6**

* **Exempel på AES-kryptering (kräver Flash Player version 17.0.0.134)**

Samplingsbaserad AES-kryptering stöds nu.

**1.4.2**

* **Video Heartbeats Library (VHL) update to version 1.4.0.1**

   * Lagt till möjlighet att paketera olika analysanvändningsfall, från andra SDK:er eller spelare, med Adobe Analytics Video Essentials.
   * Annonsspårning har optimerats genom att metoderna trackAdBreakStart och trackAdBreakComplete har tagits bort. Annonsbrytningen härleds från metodanropen trackAdStart och trackAdComplete.
   * Spelhuvudegenskapen behövs inte längre när annonser spåras.

**1.4.0**

* **Svartsignalering med alternativ innehållsersättningSom en del av TVSDK-uppdateringen (1.4) har TVSDK nu också stöd för att börja och återgå från regionala utfall mot linjärt innehåll.** TVSDK kan nu bearbeta två manifestfiler parallellt, i huvudversion och alternativt, för att övervaka utpressningssignaler även när alternativ programmering visas i stället för den ursprungliga programmeringen.

* **Ta bort/ersätt C3** AdsNu behövs inget ytterligare förberedelsearbete för att dynamiskt infoga nya annonser i VOD-resurser (video-on-demand) som kommer ut från C3-fönstret. TVSDK erbjuder nu ett API för att ta bort anpassade innehållsområden och dynamiskt infoga nya annonser. Den här kraftfulla nya funktionen är också användbar i fall där live/linjärt innehåll möts under sändning och omedelbart tas ned för användning som on demand-innehåll utan att man behöver ägna tid åt att&quot;rensa&quot; materialet.

## Lösta problem {#resolved-issues}

>[!NOTE]
>
>Alla TVSDK-kunder som använder CRS bör uppgradera till åtminstone TVSDK 1.4.32 på iOS, Android och Desktop HLS. Uppgraderingen ersätter den befintliga appimplementeringen. Efter uppgraderingen söker du efter CRS Creative URL-begäranden i ett proxyverktyg (till exempel Charles) för att kontrollera att versionen i sökvägen återspeglar version 3.1. Till exempel:
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Version 1.4.41**

* Zendesk #33777 - Localhost token-SWF för DHLS-distribution har gått ut.

   Uppdaterar localhost-token för PMP-demo på DHLS.

### Lösta problem i tidigare versioner {#resolved-issues-previous}

**Version 1.4.38** (891)

* Zendesk #30731 - TVSDK spelar inte upp flera VPAID-annonser i en AdBreak.

   Korrigerad uppspelning av flera VPAID-annonser i en AdBreak.

* Zendesk #29968 - Double Billboard.

   Videospelaren kan upprepa det sista segmentet i en punkt när en ABR-växling inträffar. På grund av detta upprepas ibland det sista segmentet i inledningen. Den här har åtgärdats.

**Version 1.4.35** (879)

* Zendesk #26058 - Stöder ANE VPAID-händelser

**Version 1.4.33** (873)

* Zendesk #21701 - Skicka den ursprungliga kreativa URL:en för 1401 CRS-begäran i stället för den normaliserade URL:en.

   Problemet där redan ompaketerade URL:er begärs för omkodning har korrigerats enligt kraven från CRS-serverdelen.
* Zendesk #26197 - Anamorfisk komprimering spelas inte upp i önskad skärmupplösning.

   **Obs**: För det här problemet krävs Flash Player 24.0.0.194 eller senare.

   Problemet där saknade poster i proportionstabellerna användes för att beräkna utdatabredden har åtgärdats.

* Zendesk #26840 - HDCP-identifiering misslyckas på IE11 + Windows7 efter andra försöket.

   **Obs**: För det här problemet krävs Flash Player 24.0.0.218 eller senare.

   Problemet löstes genom att ändra AdobeCP:s huvudmeddelandeköhantering så att den itereras genom hela kön, i stället för att bara blockera det första meddelandet.

* Zendesk #27460 - Det nya Akamai-kontot kan inte hantera en CDN-begäran för POST.

   Det nya CDN-kontot kan inte hantera en CDN-begäran för POST. Problemet löstes genom att koden uppdaterades så att annonsbegäran cdn.audiude.com blev GET istället för POST.
* Zendesk #27619 - Flash kraschar i Windows 10

   **Obs**: För det här problemet krävs Flash Player 24.0.0.218 eller senare.

   Problemet löstes genom att ett fel förhindrades på grund av långa URL:er.

* Zendesk #28218 - Spårningshändelsen utlöses inte vid återkoppling från återställningspunkten

   Det här problemet är samma problem som i Zendesk #26592. Problemet där sökåtgärder tilläts när mediespelaren är i tillståndet PREPARED för VOD-strömmar har åtgärdats.

**Version 1.4.32** (867)

* Spårningshändelse för Zendesk #26592 utlöses inte när uppspelningen startar från återställningspunkten

Koden uppdaterade inte posten för förregistrering och radbrytning när återställningspunkten inte var noll. Problemet löstes genom att logik lades till för att uppdatera koden när intervallets starttider inte matchar.

* Zendesk #27022 Ads spelas inte upp andra gången en resurs spelas upp

Undantagen med arraymetoderna har åtgärdats.

**Version 1.4.30** (855)

Följande problem löstes för TVSDK i den här versionen:

* Zendesk #22898 - Undertexter som saknas ska inte göra att uppspelningen misslyckas.

**Obs**: För det här problemet krävs Flash Player 23.0.0.185 eller senare.

Problemet löstes genom att TVSDK tilläts att fortsätta uppspelningen, även om manifestet saknar WebVTT M3U8, och bara registrera en varning.

* Zendesk #23454 - Annonser från tredje part (VPAID) hanteras inte korrekt

Problemet löstes genom att VPAID-annonser hanterades korrekt baserat på innehålls-ID:n i stället för tidsintervall.

* Zendesk #24528 - TVSDK Usage Metrics for Billing.

Viktigt: För det här problemet krävs Flash Player 23.0.0.185 eller senare.

* Zendesk # 25432 Closed Caption-problem vid storleksändring av spelaren.

Viktigt: För det här problemet krävs Flash Player 23.0.0.185 eller senare.

Koden för bildtextens visningstexturschema har fixerats för att hantera koordinaterna korrekt när spelaren ändrar storlek.

VHL (Video Heartbeat Library) har uppdaterats till version 1.5.9 för att lösa följande problem:

* Zendesk #23730 - Bithastighetsmått är tomma

Problemet löstes genom att man spårade ändringar i bithastigheten i VideoAnalyticsTracker.

* Ett nytt API, assetDuration, har lagts till i PTVideoAnalyticsTrackingMetadata för att uppdatera resursens varaktighet för direktuppspelning/linjär direktuppspelning.

**Version 1.4.28** (848)

* Zendesk #25027 - Auditude fungerar inte i skrivbordsversionen 1.4.27

Problemet löstes genom att koden lades till för att kontrollera AUDITUDE_METADATA_KEY och genom att AUDITUDE_METADATA_KEY och ADVERTISING_METADATA_KEY blev utbytbara.

* Zendesk #24428 - Vanligt buffringsproblem med användning av TVSDK för att spela upp en DRM HLS

Problemet löstes genom att man tog hänsyn till att TVSDK kan snabba upp bearbetningen när annonsinställningarna saknas genom att eliminera spärrning av annonser i förväg och spärrning av livereservationer på tidslinjen som är avsedd att synkronisera annonsinfogning.

* Zendesk #24344 - Inaktivera WebVTT-filer för att förbättra starttiderna.

**Obs**: För det här problemet krävs Flash Player 23 eller senare.

Problemet löstes genom att WebVTT-filerna lästes endast in när bildtexter måste visas.

* Zendesk #24994 - Textning för hörselskadade tas bort från spelaren vid återgång från reklamavbrott

**Obs**: För det här problemet krävs Flash Player 23 eller senare.

Den falska EOC-koden gjorde att bildtextvisningen försvann. Problemet löstes genom att de 608 bildtexskoderna RU2, RU3 och RU4 tvingades att ge korrekt synlighet i det aktuella aktiva fönstret.

**Version 1.4.27** (844)

* Zendesk #21554 - TVSDK-felfyrar utlöses inte för programtypen = video/mp4

Problemet löstes genom att TVSDK aktiverade att pinga rätt URL för felspårning i ogiltiga resursformat.

* Zendesk #23402 - Ofullständig annonsuppspelning

**Obs**: För det här problemet krävs Flash Player 23 eller senare.

Efter att ha fått ett 404-fel på vissa begäranden kan en krasch inträffa. Problemet har lösts genom att anslutningen inte stängs av medan svaret hanteras. Upplösningen ser till att VPAID-annonserna inte räknas felaktigt, så de släpps inte när de hämtas.

* Zendesk #23621 - Försök igen misslyckas på 400 och 404

**Obs**: För det här problemet krävs Flash Player 23 eller senare.

Ett problem som orsakade att DRM-metadata skadades vid växling mellan olika profiler har åtgärdats.

* Zendesk #23705 - Video Ads fryser under AdStitched break

**Obs**: För det här problemet krävs Flash Player 23 eller senare.

Det här problemet är samma problem som i Zendesk #23621.

* Zendesk #23905 - Vissa annonsbrytningar hoppar över annonsbrytningar

**Obs**: För det här problemet krävs Flash Player 23 eller senare.

Den systemspecifika nätverkskoden för Windows har åtgärdats för att säkerställa att anslutningar inte stänger referenser som för närvarande används av andra anslutningar.

* Biljett nr 24029 - HLS FER-strömmar spelar inte upp alla annonser i mellanrullen i .json-filen.

Problemet löstes genom att klienterna fick ange anpassade parametrar separat för säljprojektsinstansen så att klienterna inte behöver åsidosätta OpportunityGenerator.

**Version 1.4.26** (839)

* Zendesk #18854 - Uppdatera logik för kreativt urval baserat på CRS-regler
   * Tillhandahöll stöd för att uppdatera logiken för kreativt urval baserat på CRS-regler

* Zendesk #22725 - playbackManager.beginPlayback() implementation i exempelprogrammet för skrivbordet

   * Åtgärdade genom att ta bort det här redundanta anropet i slutet av startPlaybackFromFlashVars när metoden anropas från setupVideo()

* Zendesk #22807 - SeekManager null-referensundantag

   * Åtgärdat genom att tillhandahålla nödvändigt NULL-pekarskydd inuti SeekManager relaterat till _dispatcher

* Zendesk #22822 - Vanlig buffring när TVSDK används för att spela upp en klar HLS

   * Åtgärdat genom att ta bort den inledande affärsmöjligheten som genererats av adSignalingModeOpportunityGenerator om det inte finns någon annons

* Zendesk #23378 - Stream integrity blocks rules.xml

   * Åtgärdat genom att läsa in filen rules.xml via arbetsflödet för strömintegritet

**Version 1.4.24** (817)

* Zendesk #19851 - När spelaren anpassas till en annan bithastighet hoppar den tillbaka några bildrutor i tiden på den nya bithastigheten och ger en besvärlig upplevelse

**Obs**: För det här problemet krävs Flash Player 22.0.0.175 eller senare.

Problemet där DRM-kortet återställs efter att en liten del av ett segment har laddats ned har inte återställts korrekt.

* Zendesk #20784 - Analytics: Utlösande av innehåll för live-videoövergångar

Problemet löstes genom att ett API (trackVideoComplete) lades till för att manuellt aktivera slutförandet av innehållet under en LINEAR/LIVE-videospårningssession.

Följande bibliotek uppdaterades:

* Zendesk #21643 - VPAID-annonser spelas inte upp fullständigt

   * AdobeMobile-bibliotek till 4.10.0
   * VHL-bibliotek till 1.5.6
   * Biblioteket VHL-Nielsen till 1.6.7

Problemet löstes genom att en visningsruta i nollhöjd användes för att fylla scenen när en VPAID-annons spelas upp.

* Zendesk #22110 - Analytics: Lägga till ett h:sc:ssl-fält i hjärtslagets spårningsanrop

SSL-relaterade problem har korrigerats och VHL-biblioteket som används i TVSDK har uppdaterats till den senaste versionen.

* Zendesk #22608 - Video visar ibland en svart skärm (kräver Flash Player 22.0.0.175 eller senare)

Vid adaptiv bithastighet, med den maximala bithastigheten, visas ibland en svart skärm när videon läses in igen, även om klienten ser uppdateringar till positionen och klienten uppför sig som om den spelar upp innehållet.

**Version 1.4.23** (809)

* Zendesk #2887 - Post-roll ad skipping issue when Ad Rule logic applied to the TVSDK

**Obs**: För det här problemet krävs Flash Player 21.0.0.240 eller senare.

Problemet där annonser efter registrering hoppades över när logiken för annonseringsregler tillämpades på TVSDK har åtgärdats.

* Zendesk #19863 - Annons med VPAID-mediefil ignorerad

Om en stor intern annons har flera mediefiler med en VPAID-annons som första annons, spelas inte den infogade annonsen upp för liveströmmar. Problemet löstes genom att en annan mediefil plockades upp i stället.

* Zendesk #21021 - Late Binding Audio orsakar upprepningar av ljudsegment

**Obs**: För det här problemet krävs Flash Player 21.0.0.240 eller senare.

Det upprepade problemet med ljud har åtgärdats.

* Zendesk #21125 - Return from live/linear ad ad break early

**Obs**: För det här problemet krävs Flash Player 21.0.0.240 eller senare.

Den här versionen har stöd för att gå tillbaka från en annonsbrytning tidigt innan annonsbrytningen spelas upp tills den är klar. Tidig retur anges med en anpassad manifesttagg.

* Zendesk # 21369 Sena ljudbindningar orsakar en inkonsekvent tid

**Obs**: För det här problemet krävs Flash Player 21.0.0.240 eller senare.

Problemet har också åtgärdats genom att ljudet upprepades igen.

* Zendesk #21760, 20921 - Audio Video Desync on Seek.

**Obs**: För det här problemet krävs Flash Player 21.0.0.240 eller senare.

Det upprepade problemet med ljud har åtgärdats.

* Zendesk #22024 - Fel vid körning av TVSDK

Problemet där referensspelaren inte spelade någon ström och utlöste ett undantag vid start har åtgärdats.

**Version 1.4.22** (791)

* Zendesk #17580 - Primetime runtime-fel med kod 3357

**Obs**: För det här problemet krävs Flash Player 21.0.0.197 eller senare.

De slumpmässiga 3357 felen som inträffade genom att enhetens ID initierades korrekt när storeVoucher() anropades har åtgärdats.

* Zendesk #21334 - TVSDK-annonsbegärans timeout-värde för annonsförfrågningar från tredje part

I den här versionen har tidsgränsen för global annonsbegäran lagts till.

**Version 1.4.21** (782)

* Zendesk #19580 TVSDK väntar på att innehållsmatcharen ska slutföras innan `PTTimedMetadataChangedNotification`-meddelanden skickas

**Obs**: För det här problemet krävs Flash Player 21.0.0.182 eller senare.

Problemet löstes i Skrivbordsreferensspelaren genom att man kunde ställa in Ad-taggar och lägga till en anpassad affärsmöjlighetsgenerator som visar hur man prenumererar på anpassade cues och hur dessa behandlas i en VOD-fil.

* Zendesk #20806 Future mitroll ads in DVR window will not trigger after Swapping cams

**Obs**: För det här problemet krävs Flash Player 21.0.0.182 eller senare.

Problemet löstes genom att appen uppdaterades för att ställa in _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, &quot;false&quot;) för att inaktivera annonsinfogning före registrering i en PIP-växling, vilket resulterar i att ingen möjlighet skapas före registrering.

En sorteringsfunktion introducerades för att åtgärda den osekventiella annonsplaceringen som resulterade i en negativ varaktighet för huvudinnehållet.

* Zendesk #20522: Det går inte att hoppa över VPAID 2.0-annonser

**Obs**: För det här problemet krävs Flash Player 21.0.0.182 eller senare.

* Problemet löstes genom att man hoppade över VPAID-annonser när annonserna var giltiga.
* När adbreak-principen är inställd på att hoppa över, skickas fortfarande händelser för annonsradbrytningar. Spelarläget är inkonsekvent.

Problemet löstes så att det betedde sig korrekt och inte skickar några händelser när annonsbrytning hoppas över.

* Zendesk #20955 Ange nyckelvärdepar i egenskapen customParameters via affärsmöjlighetsgeneratorn

**Obs**: För det här problemet krävs Flash Player 21.0.0.182 eller senare.

Auditude-begäran tolkar AuditudeSettings för anpassade parametrar när en annonsenhet skapas för annonsförfrågningar.

Det här beteendet ändrades för att inkludera anpassade parametrar från objektet säljprojekt i begäran. Flera möjligheter med olika anpassade parametrar kan inte packas i en Auditude-begäran.

* Zendesk #21227 - m3u8 kan inte spelas upp enhetligt

**Obs**: För det här problemet krävs Flash Player 21.0.0.211 eller senare.

Problemet löstes genom att TVSDK kunde ignorera manifestet (HLS-underprofiler) som innehåller AC3-kodeken som TVSDK inte stöder (surround).

**Version 1.4.20** (762)

* Zendesk #19181 - Trick play fast forward to live point locks up stream.

**Obs**: För det här problemet krävs Flash Player 20.0.0.306 eller senare.

* Zendesk #19286 - Flash Player kraschade vid sökning fram och tillbaka i en FER-ström.

**Obs**: För det här problemet krävs Flash Player 20.0.0.306 eller senare.

De tillfälliga hängningar som uppstod vid sökning i Google Chrome löstes genom att frågorna stängdes av, om frågorna tar för lång tid att få ett svar eller om socketen stängs av.

* Zendesk #19305 - Khoppy-uppspelning påträffades vid uppspelning av en ström med A/V-avbrott.

**Obs**: För det här problemet krävs Flash Player 20.0.0.306 eller senare.

Problemet löstes genom att en varning rapporterades.

* Zendesk # 19359 - Flash Player kraschade på grund av positionen för #EXT-X-FAXS-CM: -attribut i ett manifest på angiven nivå.

Problemet löstes när taggen #EXT-X-FAXS-CM visas i den övre spellistan före enskilda bithastigheter eller segment i spellistan.

* Zendesk #19489 - Fast Forward to Live Point stalls plugin (live stream)

Problemet är detsamma som Zendesk #19181.

* Zendesk #19699 - TVSDK växlar inte mellan undertextspår för WebVTT

Problemet löstes genom att spelardumpen gjordes och manifestet lästes in igen när ett spår ändras och genom att det UTF8-strängkonverteringsproblem som påverkade WebVTT-bildtextens dubbelbyte-namn korrigerades.

**Version 1.4.19** (1.4.19.738)

* Zendesk #18234 - Flash Player kraschar vid uppspelning av strömmar med Unicode-strängar i CC

Det här problemet kräver Flash Player FP 20.0.0.267 eller senare och löstes genom att Unicode-strängen hanterades korrekt.

* Zendesk #18304 - Stream Integrity Support for VPAID Ads

Den här funktionen kräver Flash Player FP 20.0.0.267 eller senare och introducerades i version 1.4.19.

* Zendesk #18766 - Referensspelaren kan inte visa icke-latinska unicode-tecken i CC-spårnamn

Den här funktionen kräver Flash Player FP 20.0.0.267 eller senare och har korrigerats genom att Unicode-strängen hanterades korrekt.

* Zendesk #18804 - Spelaren kraschar i Firefox 42

Det här problemet kräver Flash Player FP 20.0.0.235 eller senare och är samma problem som Zendesk #18723.

* Zendesk #18864 - Insticksprogrammet Flash Player kraschar

Det här problemet kräver Flash Player FP 20.0.0.235 eller senare och är samma som Zendesk #18723.

* Zendesk #18998 - Om tidsstämplarna för ljud och video inte stämmer överens så har en oändlig nedladdning av segment vid avbrott gjorts.

Problemet löstes genom att man ignorerade mellanrummet mellan tidsstämplar och att bara spela upp det hämtade innehållet.

* Zendesk #19093 - Mid-roll-annonser kan bara ses en gång med liveinnehåll och FER-innehåll (full-event replay), men dessa annonser kunde inte ses igen när man snabbspolar framåt eller söker förbi annonserna

I Primetimes standardväljare för annonsprinciper flyttas inte adBreak till den önskade positionen när du slutför en sökning, om en annons i mellanrullen visas. Om du vill spela upp annonsen igen efter sökningen måste programmet åsidosätta funktionen selectAdBreaksToPlay().

* Zendesk #19101 - Rewinding into unresolved Midroll ads removes the ads placement.

Problemet löstes genom att spelaren kunde uppdatera playbackMetrics-tiden, minimumOpportunityTime och tidslinjen.

* Zendesk #19102 - Issues with FER and trick mode

Det här problemet kräver Flash Player FP 20.0.0.267 eller senare och löstes genom att fel anges för advertisingMetadata.adSignalingMode.

* Zendesk #19175 - Ibland visas inte annonser som spelas upp första gången.

Problemet löstes genom att ett nytt API, adRequestTimeout, lades till i AuditudeSettings för en tidsgräns för annonsbegäran. Användare kan nu åsidosätta standardtidsgränsen för 10-talsbegäranden.

**Version 1.4.18** (1.4.18.722)

* Zendesk #3324 - Primetimes annonseringsrapportering spårar inte annonsbrytningar när det inte finns några annonseringsmedier i en VMAP.

När en annonsbrytning är tom fästs inte annonsbrytningens start- och slutspårningshändelserna. Problemet löstes genom att man skickade startpunkter för annonsbrytningar på tomma annonsbrytningar, som VMAP AdBreak, med en giltig AdSource-nod.

**Version 1.4.17** (1.4.17.702)

* Zendesk #17168 - Bildtexter visas inte på 10 sekunder eller så efter att synligheten har växlats

Problemet löstes genom stöd för taggen EXT-X-MEDIA-TIME för VTT-bildtextsfiler.

* Zendesk #17983 - Om det inte går att hämta nycklar för ett manifest misslyckas hela manifestuppspelningen

**Obs**: Du måste ha minst Flash Player FP 19.0.0.245 eller senare.

Ibland kan det finnas ogiltiga nycklar i manifestet (t.ex. för mörka öppningar), men andra tidsintervall kan ha giltiga nycklar och kommer fortfarande att spelas upp. Tidigare misslyckades hela manifestet när en nyckel som fanns i ett manifest inte kunde hämtas. Manifestet misslyckas nu bara när alla nycklar i listan inte kan hämtas. Om vissa nycklar är giltiga, men vissa av dessa nycklar inte kunde hämtas, spelas innehållet upp. Vi kommer fortfarande att misslyckas om vi försöker spela upp ett segment som kräver en nyckel som vi inte har.

* Zendesk #18554 - Stream Integrity trimmar ner cookies i vissa fall

**Obs**: Du måste ha minst Flash Player FP 19.0.0.245 eller senare.

Ett fel i koden för cookie-manipulering som kan korta av cookie-värden har korrigerats.

**Version 1.4.16** (1.4.16.684)

* Zendesk #3732 - Lägg till stöd för proxies i Chrome för Stream Integrity (kräver Flash Player FP 19.0.0.207 eller senare)

Det här är en förbättring.

* Zendesk #4244 - Direktuppspelningsproblem vid PTS-överrullning

Problemet löstes genom att överrullning upptäcktes och diskontinuiteten per nyttolasttyp hanterades - inte generellt.

* Zendesk #4487 - Tracking Linear Channel of Content

Problemet löstes genom att spårningsfunktionen för pulsslag återinitierades under en linjär direktuppspelningssession.

* Zendesk #17427 - Adobe Stream Integrity not working through a proxy on Chrome (Win7) ()

**Obs**: Upplösningen kräver Flash Player FP 19.0.0.207 eller senare.

Problemet är detsamma som Zendesk #3732.

* Zendesk #17907 - Lag on pHLS Live Stream with Flash Player 19

**Obs**: Upplösningen kräver Flash Player FP 19.0.0.207 eller senare.

Problemet löstes genom hantering av liveströmmar där domänerna för TS-filerna ändras när livemanifestet läses in igen och filerna hämtades två gånger.

* Zendesk #17931 - HLS-innehåll med skiffer i början misslyckas med uppspelningen

**Obs**: Upplösningen kräver Flash Player FP 19.0.0.207 eller senare.

Problemet löstes genom att strömmar utan ljud hanterades under de första två sekunderna i TS-filen.

* Zendesk #17934 - Direktuppspelningsfel med Flash 19.0.0.185

**Obs**: Upplösningen kräver Flash Player FP 19.0.0.207 eller senare.

Problemet löstes genom hantering av liveströmmar med tidsinterpolering mellan ljud- och videobildrutor på segmentgränser.

* Zendesk #17973 - Latest Flash Player 19.0.0.185 kraschar under mittrullning

**Obs**: Upplösningen kräver Flash Player FP 19.0.0.207 eller senare.

Problemet löstes genom hantering av omultiplexat ljud med annonsinfogning i mellanrullen. (Tolkningsväxeln inträffar och när som helst under uppspelningen överförs innehållet till annonsen i mitten av rullen, eller mitt i annonsuppspelningen osv.)

* Zendesk #18049 - Flash 19 kraschar med Firefox 42 beta

Problemet är detsamma som Zendesk #17973.

**Version 1.4.15** (1.4.15.678)

* Zendesk #4377: Ge eld åt AD_BREAK_SKIPPED-händelsen när en annonsbrytning hoppas över på grund av annonsprincipen.

Korrigeringen var att lägga till AD_BREAK_SKIPPED om en annons hoppades över.

* Zendesk #4496 - Stream Integrity: Fel 102100 med omdirigeringar till tokeniserade strömmar.

Korrigeringen var att lägga till stöd för inställning av egenskapen useCookieHeaderForAllRequests för AVNetworkConfiguration via TVSDK.

* Zendesk #17179 - Flash-spelaren kraschar vid flera SAP-ändringar för krypterat innehåll.

En krasch under uppspelning av visst krypterat innehåll har åtgärdats.

**Obs**: Flash Player 19.0.0.200 eller senare krävs för korrigeringen.

* Zendesk #17499 - How do we not remove midrolls after watch but remove preroll from fer content

En typ har lagts till i AdBreakTimelineItem (AdBreakTimelineItem.placementType) så att AdPolicySelector kan returnera en annan princip för pre-roll-, middle-roll- och post-roll-innehåll.

* Zendesk #17665 - Bandbreddsbegränsning

Korrigeringen var att ta bort logiken för att ändra målbuffertstorleken till den ursprungliga buffertstorleken när buffringen börjar.

**Version 1.14.14** (1.4.14.771)

* Zendesk #17363 - Fix README documentation for reference player

   * Tydliga instruktioner för att hämta och installera playerglobal.swc.
   * Lägg till instruktioner för att uppdatera projektkonfigurationen med en specifik Flash Player-version.
   * Uppdatera AdvertisingOverlay-projektkonfigurationen så att lägsta spelarversion används.
   * Uppdatera ReferenceCore-projektkonfigurationen så att den använder den specifika spelarversionen 11.9

* Zendesk #17471 - Player Freezes

Delvis korrigering för ett problem där en annons inte spelas upp från början efter sökning.

* Zendesk #17496 - Podbuster är inte löst när du söker tillbaka i DVR-fönstret

Ange anpassade parametrar för varje annonsbrytning.

**Version 1.4.13** (1.4.13.660)

* Zendesk #4037 - Inget användbart profilfel (kräver Flash Player 18.0.0.232 eller senare)

åtgärda url-tolkningsproblem när frågeparametern innehåller &quot;http&quot;

* Zendesk #4260 - Flash Player 18 kraschar i IE11 (kräver Flash Player 18.0.0.232 eller senare)

Korrigerade en krasch vid uppspelning av video i helskärmsläge med IE11

* Zendesk #4262 - Adobe Primetime Player kraschar i Windows 10 (kräver Flash Player 18.0.0.232 eller senare)

Korrigerade en krasch vid uppspelning av video i helskärmsläge med FireFox i Windows.

* Zendesk #4279 - HLS TVSDK ad insertion -302 redirect issue on iOS and Desktop

Ett problem har korrigerats där en URL inte fick sin typ godkänd korrekt eftersom den inte hade något tillägg

* Zendesk #4306 - Flash Player kraschar endast vid helskärmsläge på Win (kräver Flash Player 18.0.0.232 eller senare)

Korrigerade en krasch vid uppspelning av video i helskärmsläge i Windows.

* Zendesk #4480 - ID3-tagghändelser saknas (kräver Flash Player 18.0.0.232 eller senare)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI and CRS | Förbättra: Hantera dynamiska element i vissa URL-adresser för mediefiler.

Uppdaterad Creative Repackaging Service för att hantera annonser med dynamiska kreativa URL:er.

* PTPLAY - 2114 - Stöd för MP4-uppspelning.

Grundläggande uppspelning av MP4-innehåll stöds nu, inklusive uppspelning, paus och sökning.

Följande kräver Flash Player 18.0.0.225 eller senare:

* Zendesk #3992 - Additional TrickPlay speed.

TrickPlay godkänner nu frekvenser över 16x: +/- 32, +/-64 och +/-128.

* Zendesk #3113 - Flash Player Plugin kraschar

Korrigerad krasch vid försök att spela upp en omdirigeringsannons i Mac Firefox.

* Zendesk #4037 - Inget användbart profilfel
* Zendesk #4262 - Adobe Primetime Player kraschar i Windows 10

Korrigerad krasch i Windows Firefox vid uppspelning i helskärmsläge.

**Version 1.4.11** (1.4.11.648)

* Zendesk #1869 - Issue Changing Font Size (requires Flash Player 18.0.0.200)

Tillåt att bildtextstorlekar används i WebVTT-bildtextkod.

* Zendesk #3113 - Flash Player Plugin kraschar (kräver Flash Player 18.0.0.200)
* Zendesk #3268 - Desktop: Videospelaren börjar flimra efter +- 40/50 sekunder och börjar bli svart efter +- 90 sekunder (kräver Flash Player 18.0.0.200)

Åtgärda videobaset.

* Zendesk #3670 - INVALID_PARAMETER-fel i VOD vid sökning i referensspelaren (kräver Flash Player 18.0.0.200)

InvalidateProfiles i ThreadSeek när en ny period identifieras.

* Zendesk #3896 - Flash Player kraschar med strömintegriteten inställd på ON i Chrome (kräver Flash Player 18.0.0.200)

Korrigerad krasch i inbyggt nätverksläge i pepper

* Zendesk #3905 - TVSDK-spelaren läses inte in när den finns på CDN

Ett problem med att hitta jokertecken när pageDomain inte är samma som swf-domänen har åtgärdats.

**Version 1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player kraschar Flash i Firefox

Korrigerade en tillfällig Flash Player-krasch med Firefox på Mac när en direktuppspelning på en extern bildskärm skulle växla till en strömning med högre bithastighet.(kräver Flash Player 18.0.0.160)

* Zendesk #3268 - Desktop: Videospelaren flimrar efter `+-` 40/50 sekunder och börjar bli svart efter `+-` 90 sekunder

Korrigerade ett problem i Mac Chrome där strömmen skulle börja flimra och slutligen bli svart. (kräver Flash Player 18.0.0.161)

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]`-makro fylls inte i

   * felkod 400 visas om annonsen är intern och har dålig kreativitet.
   * `[ERRORCODE]` makrot kommer att vara URL-kodat

* Zendesk #3601 - Enhancement request: Hantering av wrapper-tillägg

   * TVSDK visar omslutningstillbehör som innehåller resurser (html, iframe eller static) som stängs till textbundna. (om den infogade texten inte innehåller någon för den storleken)
   * Omslutare som har en resurs ignoreras om de inte används för visning. (används inte för spårning)
   * Endast wrapper-följeslagare med NO-resurs används för spårningsändamål. (följeslagare som bara innehåller spärra/knip)

**Version 1.4.9**

* Zendesk #2615 - issue removing HLS view from desktop display

Metoden clearVideo() har lagts till i MediaPlayer. Rensar den visade videobildrutan genom att rensa AVStream från StageVideo-objektet. Ska bara anropas om videon pausas och replaceCurrentResource eller replaceCurrentItem måste anropas innan play() kan anropas igen.

* Zendesk #3169 - Uppdatera referensspelare med Adobe Analytics-integrering

Referensspelaren har uppdaterats med Adobe Analytics-integrering

* Zendesk #3296 - Desktop HLS TVSDK - VAST, annonser från tredje part som inte spelas

Mime-typer för HLS-formatet var skiftlägeskänsliga, vilket var felaktigt och har ändrats så att de inte längre är skiftlägeskänsliga

**Version 1.4.8**

* Zendesk #2737 - Desktop Player - Error 106000 (requires Flash Player 17.0.0.184)
* Zendesk #3007 - Pre-roll-annonser visas inte efter uppdatering till Flash Player 17 (kräver Flash Player 17.0.0.184)
* Zendesk #3085 - Desktop HLS Player genererar 106000-fel efter 60 sekunder (kräver Flash Player 17.0.0.184)

**Version 1.4.7**

* Zendesk #2760 - Taggen DISCONTINUITY ignoreras i TrickPlay-läge (kräver Flash Player version 17.0.0.158)
* Zendesk #2760 - Taggen DISCONTINUITY ignoreras i TrickPlay-läge (kräver Flash Player version 17.0.0.158)

**Version 1.4.6**

* Zendesk #2652 - Auditude-dokumentation för datorns HLS, Clarified Auditude media_id for desktop HLS-dokumentation

**Version 1.4.5**

* Zendesk #2256 - Åtkomst till Överordnad Playlist, uppdaterad PSDK för att skicka timedMetadata-händelser för prenumerationstaggar i den överordnad spellistan. (kräver Flash Player version 17.0.0.134)
* Zendesk #2417 - spelaren som försökte hämta undertexter innan uppspelningen startades använde WebVTT fel segmentnummervariabel för segmentnummermatchning. Fel visas bara för media med segmentindex som börjar på noll. (kräver Flash Player version 17.0.0.134)
* Zendesk #2537 - Flash-spelaren kraschar när pepper-pluginen används med Chrome (kräver Flash Player version 17.0.0.134)
* Zendesk #2547 - Arabiska undertexter: Texten ska justeras åt höger (kräver Flash Player version 17.0.0.134)

**Version 1.4.4**

* Zendesk #1561 - Sv: `[Adobe Primetime]` Uppdatering: HLS-klientbaserat failover-stöd för PROGRAM-DATE-TIME i Desktop PSDK (kräver Flash Player version 16.0.0.305 eller senare)
* Zendesk #2197 - `[Ads]` Spårning och fel
* Zendesk #2286 - Feature Request: Ange information om annonsinläsningsstatus (VPAID)
* Zendesk #2285 - Feature Request: Hoppa över och efter en angiven tidsgräns
* Fel 3921755 - Uppdatering av OpenSSL-biblioteket till version 1.0.1L i Flash Player (kräver Flash Player version 16.0.0.305 eller senare)

**Version 1.4.2**

* Zendesk #1303 - Vertical Offset for Closed Caption (kräver Flash Player version 16.0.0.235 eller senare, förväntat releasedatum: December 2014)
* Zendesk #1870 - Closed Caption Turning On &amp; Off (kräver Flash Player version 16.0.0.235 eller senare, förväntat releasedatum: December 2014)
* Zendesk #2110 - Uppspelningen fastnar efter försök att gå in i helskärmsläge under en VPAID-annons (kräver Flash Player version 16.0.0.235 eller senare, förväntat releasedatum: December 2014)
* Zendesk #2199 - `[VPAID]` Player svarar inte vid sökning efter tidigare annonsbrytning
* Zendesk #2358 - Sv: `[Analytics]` Felaktiga kapiteldata

**Version 1.4.1**

* API:t Blackouts har uppdaterats för att vara konsekvent med Android- och iOS-implementeringen.

**Version 1.4.0**

* Zendesk #1024 - Funktion för att ta bort annonser från strömmen via manifest
* Zendesk #1423 - HLS-uppspelningsfel låser Flash Player (inget fel rapporteras)
* Zendesk #1674 - ClosedCaption visas inte. Korrigera 708-bildtextvisningen när 0x03 ETX-koder saknas.

## Kända fel {#known-issues}

* Textning fungerar inte med enbart ljud eftersom bildtextsystemet behöver video för att fungera.
Utan video finns det ingen visningsrutedimension och utan visningsrutedimension kan du inte visa grafik för bildtexter.
* Strömintegriteten är något långsammare i Google Chrome på grund av begränsningar i Chrome-sandlådan.
* Om du inaktiverar autoPlay i TVSDK 1.4 kan ett DRM-fel uppstå när spelaren är inaktiv i minst en minut. Du kan lösa problemet genom att ändra `ReferenceCore.as` genom att ändra innehållet i `onPlaybackManagerPrepared` när du inaktiverar autoPlay men läser in resurser i förväg:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Version 1.4.13** PTPLAY-8501 - När VMAP returnerar två direkta MP4-annonser som inte är omkodade, spelas samma fall upp två gånger.

* **Version 1.4.2** I version 16 av Flash Player identifierades ett problem med ABR-logiken för&quot;nedbrytning&quot; efter att spelaren har försatts i en tom buffringshändelse. Problemet förhindrar att bithastigheten ändras i miljöer med dålig bandbredd när spelaren försätts i buffertläge. Om du vill undvika problemet kan du låta din app ange `BufferControlParameters.initialBufferTime` som `BufferControlParameters.playbackBufferTime` tillfälligt under buffertläget (d.v.s. för en `BufferEvent.BUFFERING_BEGIN`-händelse) och sedan återställa den till de angivna värdena för händelsen `BufferEvent.BUFFERING_END`. Fixen till det här problemet kommer att finnas i nästa patch-version av Flash Player 16.

* **Version 1.4.0**

   * PTPLAY-1634 - Samma prenumerationstagg har olika tidsstämplar i olika live-fönster. När aktiva fönster flyttas bör samma tagg i var och en av dem ha samma tidsstämplar. Men ibland har samma taggar olika tidsstämplar.
   * PTPLAY-28 - Tidslinjen i MediaPlayer innehåller inte tomma brytningar.
   * En korsdomänprincipfil (crossdomain.xml) krävs för behörighet att strömma innehåll från en annan domän. [Ställer in filen crossdomain.xml för HTTP-strömning](https://www.adobe.com/devnet/adobe-media-server/articles/cross-domain-xml-for-streaming.html).
   * Fel 3694203 - I en DVR-ström kan sökning inifrån en uppspelning i en mellanroll till en annan mellanroll-annonsfunktion leda till att webbläsaren fryser
   * Fel 3753725 - selectPolicyForSeekIntoAd tar inte hänsyn till om annonsbrytningen har bevakats
   * Fel 3754529 - Annonser före rullning tas inte bort från strömmen vid återsökning i en live DVR-ström
   * Fel 3761896 - Om sökning tillåts under annonsuppspelning justeras annonsmarkörerna om efter sökning. Tillfällig lösning är att inte använda ITEM_UPDATED-återanrop under sökning
   * Fel 3779889 - Det fullständiga anropet görs inte när slutet på tricket nås i Video Analytics
   * Fel #VA-779 - Hjärtslag för bithastighetsändring skickas inte för Förbättrad videoanalys med referensimplementering av stöd för pulsslag. Trickuppspelning implementeras inte i exempelprogrammet.

## Användbara resurser {#helpful-resources}

* Läs den fullständiga hjälpdokumentationen på [Adobe Primetime Learn &amp; Support](https://helpx.adobe.com/support/primetime.html)-sidan.
