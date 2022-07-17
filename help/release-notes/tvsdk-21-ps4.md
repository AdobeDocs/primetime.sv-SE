---
title: Versionsinformation om TVSDK 2.1 PlayStation 4
description: Versionsinformationen för TVSDK 2.1 för PlayStation 4 beskriver de funktioner som stöds och de kända problemen i TVSDK 2.1 PlayStation 4.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 32af3fe4-c730-41f6-a558-987bd14c9bae
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# Versionsinformation om TVSDK 2.1 PlayStation 4 {#tvsdk-playstation-release-notes}

Versionsinformationen för TVSDK 2.1 för PlayStation 4 beskriver de funktioner som stöds och de kända problemen i TVSDK 2.1 PlayStation 4.

## Lösta problem {#resolved-issues}

Här är de lösta problemen för TVSDK 2.1 för PlayStation 4:

**Version 2.1.0.638**

* **PTPLAY-10439:**
När VMAP-omslutningslänken bröts fastnade spelaren i Förberedelseläge (den skickade inte 
`onComplete` till dess anropare).

* **PTPLAY-10179:**

   `creativeRepackaging` och `fallbackOnInvalidCreative` är nu inaktiverade som standard. När `creativeRepackaging` flaggan har angetts men inte `creativeRepackaging` format angavs, `onRepackagingComplete` anropades så många gånger som det fanns annonser i annonsuppdelningen, vilket gjorde att annonsbrytningar skapades flera gånger.

* **Zendesk #10304**: Variabeln för annons för aktivering/inaktivering initierades inte. Vi initierar nu variabeln från `DataSetEntry's` vektor.

* **PTPLAY-10318:**
Stöd för bakgrundsläge har introducerats.
* **Zendesk # 17409:**
När uppspelningsläget för trick försätts i tricks, spelas sedan upp i normalt uppspelningsläge igen, hoppade uppspelningspositionen.
* **PTPLAY-9552:**
När XML-svarsfiler har tolkats fästs felkoden 1108 nu när det inte finns några annonser.
* **PTPLAY-9551:**
När ingen annonsbrytning sker efter Auditude-bearbetningen anropas CRS 
**onPrefetchComplete** som minskar groupCount. Eftersom det inte finns någon annonsbrytning är **groupCount** är 0 och minskar med 1. Tidigare **groupCount** var **uint32_t** därför att det tidigare ändrades till max. Det här är nu **int32_t**.

**Version 2.1.0.621**

* **Zendesk #4555**
Direktinstallation av minnesproblem - fel som leder till inläsning - 
`MediaItemLoader` Åtgärda krascher när du släpper `mediaitemloader`

* **Zendesk #17223**
2.x CSAI: Inte alla URL:er för annonsspårning utlöses
   * Vissa VAST-annonser som i sin tur pekar på en intern och saknade spårnings-URL:er.
   * När det finns flera insiktstaggar i en annons i VAST XML sparades bara den första intrycks-URL:en och resten ignorerades. Nu sparas och fästs alla intrycks-URL:er senare.
* **Zendesk #17224**
PS4-användaragenten flyttar primär tidsinformation till slutet av UAString
* **Zendesk #17226**
2.x CSAI: Alla annonser är inte insydda.
\
   Korrigera är att ange att tidslinjen har ändrats på grund av åtgärderna insertBy eller eraseBy, och gör en periodväxling i enlighet med detta.

* **Zendesk #17284**
   [Alla plattformar] Undertexter visas inte.\
   HLS - stöd för `EXT-X-MEDIA-TIME` -tagg för VTT-bildtextfiler.

* **Zendesk #17889**
Spela upp&quot;Vinteraktiv&quot; på PS4
\
   använt korrekt förskjutning (för färgkonvertering)

* **Zendesk #17954**
Återgångslogik för annonsering + hantering av stora
\
   Korrigerade problemet om en av Vast-omslutningarna var tom, så användes Vast-parsern för att fortsätta med bearbetningen av omslutningen.

* **Zendesk #17807**
Det går inte att komma förbi tomt stort Samma som Zendesk #3103

* **Zendesk #17865**
Reservlogik för PS4 och XBox One
\
   Samma som Zendesk #3103

**Version 2.1.0.591**

* **Zendesk #3767**
PS4-kodfragment, annonslösningen misslyckas vid bearbetning av VMAP-omdirigeringar.
* **Zendesk #4096**
PS4 CSAI: Segmenteringsfel Korrigerad krasch när TVSDK genererar segmenteringsfel när annonsbiblioteket bearbetar ett VMAP-svar.

* **Zendesk #4161**
Trickplay 16x i slutet av filmen låser fast dödläge när trickläget återgår till normal uppspelning

* **Zendesk #4208**
Slumpmässig krasch när dolda bildtexter är aktiverade på Fast minnesläcka när stängda bildtexter är aktiverade

* **Zendesk #4213**
PS4 CSAI: Ändra standardsträng för användare-agent för alla annonsrelaterade anrop Strängen User-agent skapas med samma UA-sträng som används i webbläsaren + strängen add Primetime

* **PTPLAY-7675** (internal) Transcoded ads ads ads are not playing Creative Repackaging was failed when it called within a VMAP or VAST response. Fix är att bara läsa mediefilen från annons i stället för att läsa från mediefiler om det finns omfattande annonser.

* **PTPLAY-7895** (internal) När `allowMultipleAds=false`, no ads play Fixed bug where `allowMultipleAds` parametern följdes inte korrekt.

* **PTPLAY-7896** (internt) Annonserna spelas upp i fel ordningsföljd på PS4 Korrigerat problem där annonserna inte var i den ordning som annonserna visades i XML-svaren.

* PS4 TVSDK testades på nytt i en miniapp istället för i spel.

**Version 2.1.0.563**

* **Zendesk #3868**
Har TVSDK stöd för Playstation SDK 2.5 TVSDK har nu byggts med 2.5 Playstation SDK.

* **Zendesk #4093**
targetingInfo nyckelvärdepar i Pt Ads-begäran.
\
   Ett radmatningstecken som avgränsade par med nyckel/värde lades till.

## Funktioner som stöds {#supported-features}

Följande funktioner stöds i TVSDK 2.1 för PlayStation 4:

**Version 2.1.0.621**

* Ad Fallback, Daisy chaining in ad ad selection logic (Zendesk #3103) For VAST ads (creatives) with the fallback rule enabled, the TVSDK behandlar en annons med en ogiltig MIME-typ som en tom annons och försöker använda reservannonser i stället.Du kan konfigurera vissa aspekter av reservbeteendet

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

* Se den fullständiga hjälpdokumentationen på [Adobe Primetime Läs mer &amp; Support](https://experienceleague.adobe.com/docs/primetime.html) sida.
