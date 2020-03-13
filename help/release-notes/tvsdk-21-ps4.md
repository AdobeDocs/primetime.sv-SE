---
title: Versionsinformation om TVSDK 2.1 PlayStation 4
seo-title: Versionsinformation om TVSDK 2.1 PlayStation 4
description: Versionsinformationen för TVSDK 2.1 för PlayStation 4 beskriver de funktioner som stöds och de kända problemen i TVSDK 2.1 PlayStation 4.
seo-description: Versionsinformationen för TVSDK 2.1 för PlayStation 4 beskriver de funktioner som stöds och de kända problemen i TVSDK 2.1 PlayStation 4.
uuid: 494569cf-07e2-476a-b88e-e46c9cca4cdc
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: ebfc8819-f5a9-47a2-b454-0e4e6f9e4640
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Versionsinformation om TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

Versionsinformationen för TVSDK 2.1 för PlayStation 4 beskriver de funktioner som stöds och de kända problemen i TVSDK 2.1 PlayStation 4.

## Lösta problem {#resolved-issues}

Här är de lösta problemen för TVSDK 2.1 för PlayStation 4:

**Version 2.1.0.638**

* **PTPLAY-10439:**
När VMAP-inkapslingsannonslänken bröts fastnade spelaren i tillståndet Förberedelse (den skickades inte `onComplete` till anroparen).

* **PTPLAY-10179:**
   `creativeRepackaging` och värden är nu `fallbackOnInvalidCreative` inaktiverade som standard. När `creativeRepackaging` flaggan angavs men inget `creativeRepackaging` format angavs `onRepackagingComplete` anropades den så många gånger som det fanns annonser i annonsbrytningen, vilket gjorde att annonsbrytningar skapades flera gånger.

* **Zendesk #10304**:
Variabeln för annons för aktivering/inaktivering initierades inte. Vi initierar nu variabeln från `DataSetEntry's` ctor.

* **PTPLAY-10318:**
Stöd för bakgrundsläge har introducerats.
* **Zendesk # 17409:**
När uppspelningsläget för trick försätts i tricks, spelas sedan upp i normalt uppspelningsläge igen, hoppade uppspelningspositionen.
* **PTPLAY-9552:**
När XML-svarsfiler har tolkats fästs felkoden 1108 nu när det inte finns några annonser.
* **PTPLAY-9551:**
När det inte finns någon annonsbrytning efter Auditude-bearbetningen anropar CRS **onPrefetchComplete** som minskar groupCount. Eftersom det inte finns någon annonsbrytning är **groupCount** 0 och minskar med 1. Tidigare var **groupCount** **uint32_t** på grund av vilket det brukade ändra till max-värdet. Detta är nu **int32_t**.

**Version 2.1.0.621**

* **Zendesk #4555** Instant on Memory issues leading-Loading errors - Fix for crash `MediaItemLoader` when release `mediaitemloader`

* **Zendesk #17223** 2.x CSAI: Inte alla URL:er för annonsspårning utlöses
   * Vissa VAST-annonser som i sin tur pekar på en intern och saknade spårnings-URL:er.
   * När det finns flera insiktstaggar i en annons i VAST XML sparades bara den första intrycks-URL:en och resten ignorerades. Nu sparas och fästs alla intrycks-URL:er senare.
* **Zendesk #17224** PS4 User Agent flyttar information i realtid till slutet av UAString
* **Zendesk #17226** 2.x CSAI: Alla annonser är inte insydda.\
   Korrigera är att ange att tidslinjen har ändrats på grund av åtgärderna insertBy eller eraseBy, och gör en periodväxling i enlighet med detta.

* **Zendesk #17284**
   [Alla plattformar] visas inte med undertexter.\
   HLS - stöd för taggen `EXT-X-MEDIA-TIME` för VTT-bildtextfiler.

* **Zendesk #17889** Playback &quot;Milky&quot; on PS4\
   använt korrekt förskjutning (för färgkonvertering)

* **Zendesk #17954** Ad fallback logic + hantering av enorma\
   Korrigerade problemet om en av Vast-omslutningarna var tom, så användes Vast-parsern för att fortsätta med bearbetningen av omslutningen.

* **Zendesk #17807** Det går inte att komma förbi largeSamma som Zendesk #3103

* **Zendesk #17865** Fallback Logic i PS4 och XBox One\
   Samma som Zendesk #3103

**Version 2.1.0.591**

* **Zendesk #3767** PS4 Ad code snippet, Annonsupplösning misslyckas vid bearbetning av VMAP-omdirigeringar.
* **Zendesk #4096** PS4 CSAI: SegmenteringsfelKorrigerad krasch när TVSDK genererar segmenteringsfel när annonsbiblioteket bearbetar ett VMAP-svar.

* **Zendesk #4161** Trickplay 16x i slutet av filmen låser sigFast dödläge vid återgång till normal uppspelning

* **Zendesk #4208** Slumpmässig krasch när undertexter är aktiveradeFast minnesläcka när undertexter är aktiverade

* **Zendesk #4213** PS4 CSAI: Ändra standardsträng för användare-agent för alla annonsrelaterade anropSträngen User-agent skapas med samma UA-sträng som används i webbläsaren + strängen add Primetime

* **PTPLAY-7675** (internal)Transcoded ads ads fungerar inteCreative Repackaging misslyckades vid anrop inom ett VMAP- eller VAST-svar. Fix är att bara läsa mediefilen från annons i stället för att läsa från mediefiler om det finns omfattande annonser.

* **PTPLAY-7895** (internal)When `allowMultipleAds=false`, no ads playFixed bug där `allowMultipleAds` parametern inte följdes korrekt.

* **PTPLAY-7896** (internal)Ads spelas upp i fel ordningsföljd på PS4Fixed issue where ads not in the order in the ads in the XML responses.

* PS4 TVSDK testades på nytt i en miniapp istället för i spel.

**Version 2.1.0.563**

* **Zendesk #3868** Klarar TVSDK Playstation SDK 2.5TVSDK har nu byggts med 2.5 Playstation SDK.

* **Zendesk #4093** targetingInfo key-value pairs in Pt Ads request.\
   Ett radmatningstecken som avgränsade par med nyckel/värde lades till.

## Funktioner som stöds {#supported-features}

Följande funktioner stöds i TVSDK 2.1 för PlayStation 4:

**Version 2.1.0.621**

* Ad Fallback, Daisy chaining in ad ad selection logic (Zendesk #3103)For VAST ads (creatives) with the fallback rule enabled, the TVSDK behandlar en annons med en ogiltig MIME-typ som en tom annons och försöker använda reservannonser i stället.Du kan konfigurera vissa aspekter av reservbeteendet

**Version 2.1.0.538**

* HLS VOD-uppspelning, inklusive uppspelning, paus, sökning
* Adaptiv strömning av bithastighet
* Uppspelning av krypterat innehåll med Primetime DRM och vanilla AES-skyddat innehåll
* Annonsinfogning på klientsidan med standardannonsbeteenden och annonsflexibilitet
* Kreativ ompackning
* WebVTT undertexter
* Aktivera direkt med anpassad startposition
* Trixuppspelning med snabb och snabb tillbakaspolning
* 302 omdirigering

## Användbara resurser {#helpful-resources}

* Läs den fullständiga hjälpdokumentationen på [Adobe Primetimes sida för utbildning och support](https://helpx.adobe.com/support/primetime.html) .