---
title: TVSDK-konvertering - 1.3 till 2.0 för JavaScript
seo-title: TVSDK-konvertering - 1.3 till 2.0 för JavaScript
description: Många metodsignaturer och API-elementnamn har ändrats för 2.0. Granska de här tabellerna för att se all API-ändringsinformation.
seo-description: Många metodsignaturer och API-elementnamn har ändrats för 2.0. Granska de här tabellerna för att se all API-ändringsinformation.
uuid: d2d1742d-c90c-43f5-94fc-8c4a57cb8ed4
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: c732f54d-116c-43f3-bec4-5e71af208426
translation-type: tm+mt
source-git-commit: cfd6da49e85e13e29e8458ee98231a8b476867db
workflow-type: tm+mt
source-wordcount: '5058'
ht-degree: 0%

---


# TVSDK-konvertering - 1.3 till 2.0 för JavaScript {#tvsdk-conversion-to-for-javascript}

Många metodsignaturer och API-elementnamn har ändrats för 2.0. Granska de här tabellerna för att se all API-ändringsinformation.

## Implementera återanropsfunktioner i JavaScript {#implement-callback-functions-in-javascript}

Kommentarer i metoddokumentationen föreslår signaturen för återanrop som du måste implementera.

För JavaScript baseras API-syntaxen på webb-ID. För ett TVSDK-gränssnitt kallas metodnamnen för *methodName*(). För metoder som ska implementeras av programmet läggs ett read/write-attribut med namnet ** methodNameCallbackFunc till i gränssnittet och programmet bör ange att det ska peka på en funktion som implementerar metoden. Exempel:

```shell
// An app implementable interface
interface ContentFactory
{
    /*
     * AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item);
     */
    attribute Object retrieveAdPolicySelectorCallbackFunc;
 
    /*
     * ContentResolverList retrieveResolvers(MediaPlayerItem item);
     */
    attribute Object retrieveResolversCallbackFunc;
 
    /*
     * OpportunityGeneratorList retrieveGenerators(MediaPlayerItem item);
     */
    attribute Object retrieveGeneratorsCallbackFunc;
};

// this is how to implement it
var factory = new AdobePSDK.ContentFactory();
factory.retrieveAdPolicySelectorCallbackFunc = function(item)
{
    // return your adPolicySelector according to the item
    return adPolicySelector;
}
 
mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig ();
playerConfig.adFactory = factory;
// Use this config to load new MediaResource
```

## Ändringar i arbetsflödets API-element för annonsering för 2.0 {#advertising-workflow-api-element-changes-for}

I dessa tabeller jämförs API-elementen för annonsarbetsflödet för JavaScript TVSDK mellan version 1.3 och 2.0.

Tabeller i det här avsnittet:

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ErsättTidsintervall
* Placement
* Möjligheter
* Reservation
* Tidslinje / Tidslinjeobjekt / Tidslinjemarkör
* AdBreak
* Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* TimelineOperation
* AdBreakPlacement
* AuditudeSettings

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>: interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ; <br /> const unsigned short METADATA_TYPE_ID3 = 1 ; <br /> skrivskyddat attribut utan signerad kort typ, <br /> skrivskyddat attribut, lång tid,<br /> skrivskyddat attribut DomString id;<br /> skrivskyddat attribut DOMString-namn;<br /> skrivskyddat attribut DOMString-innehåll; <br /> metadata för skrivskyddat attributobjekt,<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ;<br /> const unsigned short METADATA_TYPE_ID3 = 1 ;<br /> skrivskyddat attribut unsigned short metadataType;<br /> skrivskyddat attribut, lång tid,<br /> long id för skrivskyddat attribut,<br /> skrivskyddat attribut DOMString-namn;<br /> <br /> metadata för skrivskyddat attributobjekt,<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Ingen ändring för 2.0)</td> 
   <td><p>interface TimedMetadataList {<br /> readonly attribute unsigned long;<br /> getter TimedMetadata(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSignalingMode {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>Gränssnitt AdSignalingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CUES, <br /> const unsigned short MODE_SERVER_MAP, <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>Detta ersätter nyckeln MetadataKeys::MANIFEST_CUES.</td> 
  </tr> 
 </tbody> 
</table>

### AdvertisingMetadata {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>Interface AdvertisingMetadata { <br /> attribute AdSignalingMode; <br /> attribute AdBreakWatchedPolicy adBreakAsWatched; <br /> attribut boolesk livePreroll; <br /> attribute boolean delayAdLoading; <br /> };</p> </td> 
   <td>Den här funktionen tillhandahålls av<p>MetadataKeys::ADVERTISING_METADATA</p> nyckel.</td> 
  </tr> 
 </tbody> 
</table>

### CustomRangeMetadata {#customrangemetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>Gränssnitt CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> attribut osignerad kort typ, <br /> attribute boolean adjustSeekPosition; <br /> attribute TimeRangeList timeRangeList; <br /> };</p> </td> 
   <td>(Nytt i 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### ErsättTidsintervall {#replacetimerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface ReplaceTimeRange { <br /> attribute unsigned long begin; <br /> skrivskyddat attribut utan signerad lång ände, <br /> attributet har lång varaktighet utan tecken, <br /> attribute unsigned long replaceDuration; <br /> };</p> </td> 
   <td>(Nytt i 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Placement {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>Gränssnittsplacering { <br /> const unsigned short TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> skrivskyddat attribut utan signerad kort typ, <br /> skrivskyddat attribut, lång tid, <br /> lång skrivskyddad attributlängd, <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> skrivskyddat attribut i kort läge utan tecken, <br /> skrivskyddat attribut TimeRange-intervall; <br /> };</p> </td> 
   <td>(Nytt i 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Möjligheter {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>gränssnittsmöjlighet { <br /> readonly attribute DomString id; <br /> placering av skrivskyddade attribut, <br /> skrivskyddade objektinställningar för attribut, <br /> skrivskyddat attribut Object customParameters; <br /> }; </p> </td> 
   <td>(Nytt i 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Reservation {#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>gränssnittsreservation { <br /> readonly attribute TimeRange range; <br /> skrivskyddat attributlångt undantag, <br /> }; </p> </td> 
   <td> (Nytt i 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Tidslinje / Tidslinjeobjekt / Tidslinjemarkör {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>Tidslinje</strong>: interface Timeline <br /> { readonly attribute TimelineMarkerList timelineMarkers; <br /> skrivskyddat attribut TimelineItemList timelineItems; <br /> double convertToLocalTime( dubbel tid); <br /> double convertToVirtualTime( dubbel tid); <br /> };</p> </td> 
   <td><p>interface Timeline {<br /> readonly attribute TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>Tidslinjeobjekt</strong>: interface TimelineItem :<br /> TimelineMarker {<br /> readonly attribute long id; <br /> skrivskyddat attribut TimeRange virtualRange; <br /> skrivskyddat attribut TimeRange localRange; <br /> skrivskyddade attribut med boolesk bevakning, <br /> skrivskyddat attribut boolesk temporärt, <br /> }; </p> </td> 
   <td>(Nytt i 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>Markör</strong>för tidslinje: (Ingen ändring för 2.0)</td> 
   <td><p>interface TimelineMarker {<br /> readonly attribute double time;<br /> skrivskyddat attribut med dubbel varaktighet,<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdBreak {#adbreak}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreak {<br /> <br /><br /> <br /> readonly attribute double duration;<br /> skrivskyddade attribut AdList ads;<br /> <br /> <br /> skrivskyddat attribut AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> readonly attribute double time;<br /> skrivskyddat attribut double replaceDuration;<br /> <br /> skrivskyddat attribut med dubbel varaktighet,<br /> skrivskyddat attribut AdList adList;<br /> <br /> skrivskyddade attribut DOMString-data;<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Annons</strong>: interface Ad {<br /> readonly attribute AdAsset primaryAsset;<br /> skrivskyddat attribut AdAssetList companionAssets;<br /> <br /> skrivskyddat attribut med dubbel varaktighet,<br /> skrivskyddat attribut DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> skrivskyddat attribut osignerat kort adType;<br /> skrivskyddat attribut AdInsertionType adInsertionType; <br /> <br /> skrivskyddat attribut med boolesk klickbarhet, <br /> skrivskyddat attribut boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>interface Ad {<br /> readonly attribute AdAsset primaryAsset;<br /> skrivskyddat attribut AdAssetList companionAssets;<br /> <br /> skrivskyddat attribut med dubbel varaktighet,<br /> skrivskyddat attribut DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> skrivskyddat attribut utan signerad kort typ,<br /> skrivskyddat attribut AdInsertionType insertionType; <br /> skrivskyddad objektspårning,<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Ingen ändring för 2.0)</td> 
   <td><p>interface AdAsset {<br /> readonly attribute DomString id;<br /> skrivskyddat attribut med dubbel varaktighet,<br /> skrivskyddat attribut MediaResource-resurs,<br /> skrivskyddat attribut AdClick adClick;<br /> metadata för skrivskyddat attributobjekt,<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Ingen ändring för 2.0)</td> 
   <td><p>interface AdClick {<br /> readonly attribute DomString id;<br /> skrivskyddat attribut DOMString-titel;<br /> skrivskyddat attribut DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Ingen ändring för 2.0)</td> 
   <td><p>interface AdList {<br /> readonly attribute unsigned long length;<br /> getter Ad(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Ingen ändring för 2.0)</td> 
   <td><p>interface AdAssetList {<br /> readonly attribute unsigned long;<br /> getter AdAsset(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interface AdBannerAsset : AdAsset<br /> {<br /> readonly attribute int width;<br /> skrivskyddat attribut int height,<br /> skrivskyddat attribut DomString staticUrl;<br /> skrivskyddat attribut, DOMString-höjd;<br /> skrivskyddat attribut DOMString width;<br /> };</p> </td> 
   <td> Nytt i 2.0</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakTimelineItem / AdTimelineItem {#adbreaktimelineitem-adtimelineitem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>AdBreakTimelineItem</strong>: interface AdBreakTimelineItem : TimelineItem { <br /> readonly attribute AdBreak adBreak; <br /> skrivskyddat attribut för AdTimelineItemList-objekt; <br /> }; </p> </td> 
   <td> (Nytt i 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interface AdTimelineItem : TimelineItem { <br /> readonly attribute AdBreak adBreak; <br /> lässkyddat attribut Ad ad; <br /> }; </p> </td> 
   <td> (Nytt i 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interface AdBreakTimelineItemList { <br /> readonly attribute unsigned long; <br /> getter AdBreakTimelineItem (unsigned log index); <br /> };</p> </td> 
   <td> (Nytt i 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPolicy {<br /> readonly attribute short AD_BREAK_POLICY_SKIP;<br /> skrivskyddat attribut short AD_BREAK_POLICY_PLAY;<br /> skrivskyddat attribut short AD_BREAK_POLICY_REMOVE;<br /> skrivskyddat attribut short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> readonly attribute short AD_BREAK_POLICY_SKIP;<br /> skrivskyddat attribut short AD_BREAK_POLICY_PLAY;<br /> skrivskyddat attribut short AD_BREAK_POLICY_REMOVE;<br /> skrivskyddat attribut short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy {<br /> readonly attribute short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> skrivskyddat attribut short AD_BREAK_AS_WATCHED_ON_END;<br /> skrivskyddat attribut short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> skrivskyddat attribut short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> skrivskyddat attribut short AD_BREAK_AS_WATCHED_ON_END;<br /> skrivskyddat attribut short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> readonly attribute short AD_POLICY_PLAY;<br /> skrivskyddat attribut short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> skrivskyddat attribut short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; skrivskyddat attribut short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> skrivskyddat attribut short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> skrivskyddat attribut short AD_POLICY_PLAY;<br /> skrivskyddat attribut short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> skrivskyddat attribut short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> skrivskyddat attribut short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> skrivskyddat attribut short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> readonly attribute short AD_POLICY_MODE_PLAY;<br /> skrivskyddat attribut short AD_POLICY_MODE_SEEK;<br /> skrivskyddat attribut short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> skrivskyddat attribut short AD_POLICY_MODE_SEEK;<br /> skrivskyddat attribut short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {<br /> readonly attribute AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> skrivskyddat attribut AdTimelineItem adTimelineItem;<br /> skrivskyddat attribut double currentTime;<br /> skrivskyddat attribut double seekToTime;<br /> dubbelfrekvens för skrivskyddade attribut,<br /> skrivskyddat attributkortläge, //AdPolicyMode<br /> };</p> </td> 
   <td><p>interface AdPolicyInfo {<br /> readonly attribute AdBreakPlacementList <br /> adBreakPlacements;<br /> lässkyddat attribut Ad ad;<br /> skrivskyddat attribut double currentTime;<br /> skrivskyddat attribut double seekToTime;<br /> dubbelfrekvens för skrivskyddade attribut,<br /> skrivskyddat attributkortläge, //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimelineOperation {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface TimelineOperation { <br /> readonly attribute Placation placement; <br /> };</p> </td> 
   <td> (Nytt i 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPlacement {#adbreakplacement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPlacement : TimelineOperation {<br /> readonly attribute AdBreak adBreak;<br /> placering av skrivskyddade attribut, // Från TimelineOperation<br /> -skrivskyddat attribut vid dubbel tid;<br /> skrivskyddat attribut med dubbel varaktighet,<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> readonly attribute AdBreak adBreak;<br /> placering av skrivskyddade attribut,<br /> skrivskyddat attribut med dubbel tid,<br /> skrivskyddat attribut med dubbel varaktighet,<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AuditudeSettings {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface AuditudeSettings : AdvertisingMetadata { <br /> attribute DomString zoneId; <br /> attribute DomString mediaId; <br /> attribute DomString defaultMediaId ; <br /> attribute DomString domain; <br /> attribute Object targetInfo; <br /> attribute Object customParameters; <br /> attribute Boolean creativePackingEnabled;<br /> attribute Boolean showStaticBanners;<br /> };</p> </td> 
   <td>Funktionen tillhandahölls av MetadataKeys::AUDITUDE_METADATA_KEY-tangenten.</td> 
  </tr> 
 </tbody> 
</table>

## Ändringar av API-elementet för anpassning för 2.0 {#customization-api-element-changes-for}

I de här tabellerna jämförs API-elementen för JavaScript TVSDK mellan version 1.3 och 2.0.

Tabeller i det här avsnittet:

* MediaPlayerItemConfig
* ContentFactory
* NetworkConfiguration

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemConfig {<br /> attribute ContentFactory adFactory;<br /> attribute StringList subscribeTags;<br /> <br /> attributet StringList adTags;<br /> <br /> <br /> attribute AdSignalingMode adSignalingMode;<br /> customRangeMetadata-attributet CustomRangeMetadata;<br /> attribute NetworkConfiguration networkConfiguration;<br /> attribute AdvertisingMetadata advertisingMetadata;<br /> attribute Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> <br /><br /> - <br /> attributet StringList adTags;<br /> attribute StringList subscribedTags;<br /> attribute MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem item);<br /> */<br /> attribute Object retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem-objekt);<br /> */<br /> attribute Object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### NetworkConfiguration {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface NetworkConfiguration<br /> {<br /> attribute boolean forceNativeNetworking;<br /> attribute boolean useRedirectedUrl;<br /> attribute Object cookieHeader;<br /> booleskt attribut readSetCookieHeader;<br /> attribute int masterUpdateInterval; <br /> attributet boolean useCookieHeaderForAllRequests;<br /> attribute int readLimit;<br /> };</p> </td> 
   <td>I 1.3 fanns en del av den här funktionen från MetadataKeys</td> 
  </tr> 
 </tbody> 
</table>

## DRM API-elementändringar för 2.0 {#drm-api-element-changes-for}

I dessa tabeller jämförs DRM API-elementen för JavaScript TVSDK mellan version 1.3 och 2.0.

Tabeller i det här avsnittet:

* DRM-arbetsflödesinitiering
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### DRM-arbetsflödesinitiering {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td>Programmet måste anropa AdobePSDK.beginDRMWorkflow för att initiera DRM-arbetsflödet. Utan detta anrop spelas inte DRM-videor upp.<p>gränssnittet AdobePSDK<br /> {<br /> void initialDRMWorkFlow(<br /> DomString appStoratePath, <br /> DOMString publisherId, <br /> DOMString appId, <br /> DOMString appVersion, <br /> boolean privacyModeOn);<br /> };</p> </td> 
   <td>Initieringen utfördes internt och inget explicit anrop krävdes.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API:er | 1.3 API:er |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| Ingen ändring för 2.0. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| Ingen ändring för 2.0. | enum DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td>Ingen ändring för 2.0.</td> 
   <td><p>gränssnittet DRMMetadata<br /> {<br /> readonly-attributet DOMString serverUrl;<br /> skrivskyddat attribut DomString licenseId;<br /> skrivskyddade DRMPolicyArray-principer, <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>gränssnitt för DRMPlaybackTimeWindow {<br /> readonly-attribut för playbackPeriodInSeconds;<br /> skrivskyddat attribut long playbackStartDate;<br /> skrivskyddat attribut long playbackEndDate;<br /> };</p> </td> 
   <td><p>gränssnittet DRMPlaybackTimeWindow {<br /> readonly attribute int periodInSeconds;<br /> skrivskyddat attribut int startDate;<br /> skrivskyddat attribut int endDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td>Ingen ändring för 2.0.</td> 
   <td><p>gränssnitts-DRMLicense {<br /> skrivskyddat attribut Uint8Array-byte;<br /> skrivskyddat attribut Date licenseStartDate;<br /> skrivskyddat attribut Date licenseEndDate;<br /> skrivskyddat attribut Date offlineStorageStartDate;<br /> skrivskyddat attribut Date offlineStorageEndDate; <br /> skrivskyddat attribut DomString serverUrl;<br /> skrivskyddat attribut DomString licenseID;<br /> skrivskyddat attribut DomString policyID;<br /> skrivskyddat attribut: DRMPlaybackTimeWindow playbackTimeWindow;<br /> skrivskyddat attribut Object customProperties;<br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMLicenseDomain {<br /> readonly attribute DOMString authenticationDomain;<br /> skrivskyddat attribut DRMAuthenticationMethod authenticationMethod; <br /> skrivskyddat attribut DomString serverUrl;<br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {<br /> readonly attribute DOMString authDomain;<br /> skrivskyddat attribut: DRMAuthenticationMethod authMethod; <br /> skrivskyddat attribut DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMPolicy<br /> {<br /> readonly attribute DomString authenticationDomain;<br /> skrivskyddat attribut DRMAuthenticationMethod authenticationMethod;<br /> <br /> skrivskyddat attribut DomString displayName;<br /> skrivskyddat attribut DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interface DRMPolicy<br /> {<br /> readonly attribute DomString authDomain;<br /> skrivskyddat attribut: DRMAuthenticationMethod authMethod;<br /> skrivskyddat attribut DomString dispName;<br /> skrivskyddat attribut DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>gränssnitt för DRMManager: EventTarget {<br /> void obtainLicense(DRMMetadata-metadata, <br /> DRMAcquireLicenseSettings-inställning, <br /> DRMAquireLicenseListener-lyssnare);<br /> void obtainPreviewLicense(DRMMetadata-metadata, <br /> DRMAquireLicenseListener-lyssnare);<br /> void authenticate(DRMMetadata metadata, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString user, <br /> DomString password, <br /> DRMAuthenticateListener listener);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array-matris, DRMErrorListener-lyssnare);<br /> void initialize(DRMOperationCompleteListener listener);<br /> attribute long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener-lyssnare);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener-lyssnare);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, <br /> boolean commitOmedelbart,<br /> DRMReturnLicenseListener listener);<br /> void setAuthenticationToken(<br /> DRMMetadata-metadata, <br /> DomString authenticationDomain, <br /> Uint8Array token, <br /> DRMOperationCompleteListener-lyssnare);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener-lyssnare);<br /> };</p> </td> 
   <td><p>gränssnitt för DRMManager: EventTarget {<br /> void obtainLicense(DRMMetadata-metadata, <br /> DRMAcquireLicenseSettings-inställning, <br /> EventContext eventContext);<br /> void obtainPreviewLicense(DRMMetadata-metadata, <br /> EventContext eventContext);<br /> void authenticate(DRMMetadata metadata, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString user, <br /> DomString password, <br /> EventContext eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array-array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> attribute long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> EventContext eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> boolean commitImmedially,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> DRMMetadata-metadata, <br /> DomString authenticationDomain, <br /> Uint8Array token, <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>klassen DRMErrorListener : <br /> public psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils: PSDKString&amp; errorString, const psdkutils::PSDKString&amp; errorServerUrl) = 0; <br /><br /> <br /> skyddad:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Händelse/gränssnitt/beskrivning 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>När ett fel inträffar under någon av de asynkrona metoderna för DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>klassen DRMOperationCompleteListener : <br /> public DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete() = 0;<br /> <br /> skyddad:<br /> virtuell ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Händelse/gränssnitt/beskrivning 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>När DRM-initieringen är slutförd.</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>När åtgärden joinLicenseDomain() har slutförts.</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>När åtgärden leaveLicenseDomain() har slutförts.</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>När åtgärden resetDRM() har slutförts.</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>När åtgärden setAuthenticationTokenSet() har slutförts.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>När åtgärden storeLicenseBytes() har slutförts.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>klassen DRMAuthenticateListener : <br /> public DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> skyddad:<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
   <td>Händelse/gränssnitt/beskrivning 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>När metoden DRMManager::authenticate anropas.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>klassen DRMAquireLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> skyddad:<br /> virtuell ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Händelse/gränssnitt/beskrivning 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>När metoden DRMManager::obtainPreviewLicense har anropats.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>När metoden DRMManager::obtainLicense anropas.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>klassen DRMReturnLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtuell void onLicenseReturnComplete(uint32_t numReturned ) = 0;<br /> <br /> skyddad:<br /> virtuell ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Händelse/gränssnitt/beskrivning 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>När metoden DRMManager::returnLicense anropas.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Allmänna ändringar av API-elementet för uppspelning för 2.0 {#generic-playback-api-element-changes-for}

I dessa tabeller jämförs de generiska API-elementen för uppspelning mellan JavaScript TVSDK 1.3 och 2.0.

Tabeller i det här avsnittet:

* MediaResource
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* TextFormat
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> attribute DomString url; <br /> attribut osignerad kort typ,<br /> attributobjektmetadata;<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> attribute DomString url;<br /> Attributet DomString type;<br /> attributobjektmetadata;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( dubbel position);<br /> void play();<br /> void pause();<br /> void seek( dubbel position);<br /> void seekToLocal( dubbel position);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaPlayerItem-objekt);<br /> void replaceCurrentResource(MediaResource-resurs, <br /> MediaPlayerItemConfig-konfiguration); <br /> void ause();<br /> void restore();<br /> void notifyClick();<br /> <br /> skrivskyddat attribut TimeRange playbackRange;<br /> skrivskyddat attribut TimeRange seekableRange;<br /> skrivskyddat attribut double currentTime;<br /> skrivskyddat attribut double localTime;<br /> skrivskyddat attribut TimeRange buffedRange;<br /> skrivskyddat attribut DRMManager drmManager;<br /> skrivskyddat attribut MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> <br /> <br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> <br /> skrivskyddat attribut utan signerad kort status,<br /> <br /> attributet unsigned short volume;<br /> attribute ABRControlParameters abrControlParameters;<br /> attribute BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBLE, //For CC visibility<br /> const unsigned short INVISIBLE; //For CC visibility<br /> attribute unsigned short ccVisibility;<br /> attribute TextFormat ccStyle;<br /> skrivskyddat attribut PlaybackMetrics playbackMetrics;<br /> <br /> attributets dubbla ränta,<br /> attribute MediaPlayerView view;<br /> skrivskyddat attribut tidslinje,<br /> attribute double currentTimeUpdateInterval; <br /> // inställning this Won be supported for 2.0<br /> };</p> </td> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( int-position);<br /> void play();<br /> void pause();<br /> void seek( int position);<br /> void seekToLocalTime( int position);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaResource-källa);<br /> <br /> <br /> <br /> <br /> <br /> <br /> skrivskyddat attribut TimeRange playbackRange;<br /> skrivskyddat attribut TimeRange seekableRange;<br /> skrivskyddat attribut double currentTime;<br /> skrivskyddat attribut double localTime;<br /> skrivskyddat attribut TimeRange buffedRange;<br /> skrivskyddat attribut DRMManager drmManager;<br /> skrivskyddat attribut MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> skrivskyddat attribut utan signerat kort tillstånd,<br /> <br /> attributet unsigned short volume;<br /> attribute ABRControlParameters abrControlParameters;<br /> attribute BufferControlParameters bufferControlParameters;<br /> <br /> skrivskyddad osignerad kort VISIBLE, //For CC visibility<br /> readonly unsigned short INVISIBLE; //For CC visibility<br /> attribute unsigned short ccVisibility;<br /> attribute TextFormat ccStyle;<br /> skrivskyddat attribut PlaybackMetrics playbackMetrics;<br /> attribute MediaPlayerConfig mediaPlayerConfig;<br /> attributets dubbla ränta,<br /> attribute MediaPlayerView view;<br /> skrivskyddat attribut tidslinje,<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const unsigned short PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>(Nytt i 2.0)</td> 
  </tr> 
 </tbody> 
</table>

#### Händelser som stöds av MediaPlayer {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 Händelsenamn</th> 
   <th>2.0-gränssnitt</th> 
   <th> </th> 
   <th>1.3 Händelsenamn</th> 
   <th>1.3-gränssnitt</th> 
  </tr> 
  <tr> 
   <td><p>(borttagen för 2.0)</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>förberedd</td> 
   <td>Händelse</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>När ett mediespelarobjekt uppdateras.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>uppdaterad</p> <p>När mediespelaren har uppdaterat mediet.</p> </td> 
   <td>Händelse</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>TtmedMetadata</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>timelineUpdated</td> 
   <td>Händelse</td> 
   <td> </td> 
   <td>TidslinjeUppdaterad</td> 
   <td>Händelse</td> 
  </tr> 
  <tr> 
   <td>Borttaget i 2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>playStart</td> 
   <td>Händelse</td> 
  </tr> 
  <tr> 
   <td>Borttagen för 2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>Händelse</td> 
  </tr> 
  <tr> 
   <td>statusChanged</td> 
   <td>StatusEvent</td> 
   <td> </td> 
   <td>stateChanged</td> 
   <td>StateEvent</td> 
  </tr> 
  <tr> 
   <td>sizeAvailable</td> 
   <td>SizeEvent</td> 
   <td> </td> 
   <td>size</td> 
   <td>SizeEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakStarted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakStart</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adStarted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adStart</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
   <td> </td> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
  </tr> 
  <tr> 
   <td>adCompleted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adComplete</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakCompleted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakComplete</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>timeChanged</td> 
   <td>TimeEvent</td> 
   <td> </td> 
   <td>progress</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>Händelse</td> 
   <td> </td> 
   <td>buffert</td> 
   <td>Händelse</td> 
  </tr> 
  <tr> 
   <td>bufferingEnd</td> 
   <td>Händelse</td> 
   <td> </td> 
   <td>bufferComplete</td> 
   <td>Händelse</td> 
  </tr> 
  <tr> 
   <td>seekBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>Händelse</td> 
  </tr> 
  <tr> 
   <td>seekEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekComplete</td> 
   <td>TimeEvent</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>LoadInformationEvent</td> 
   <td> </td> 
   <td>loadInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>operationFailed</td> 
   <td>seekEvent</td> 
   <td> </td> 
   <td>operationFailed</td> 
   <td>ErrorEvent</td> 
  </tr> 
  <tr> 
   <td>drmMetadataInfoAvailable</td> 
   <td>DRMMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DRMMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>reservationReached</td> 
   <td>ReservationEvent</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>TidslinjeInnehavareHändelse</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>bitrateChanged</td> 
   <td>BitrateChangedEvent</td> 
  </tr> 
  <tr> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>ratePlay</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>ratePlay</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adClick<br /> When user clicks on an Ad.</td> 
   <td>AdClickEvent</td> 
   <td> </td> 
   <td><p>Nytt i 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> When the playback profile changes.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>Nytt i 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br /> When seek position justerar på grund av interna eller externa regler.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Nytt i 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> When a media player item is updated. För vissa strömmar som innehåller ljudspår som bara kan identifieras vid uppspelning, utlöses den här händelsen när nya ljudspår är tillgängliga.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Nytt i 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>captionsUppdaterat <br /> När ett mediespelarobjekt uppdateras. För live/linjär direktuppspelning måste klienten regelbundet uppdatera medieresursen för att kunna identifiera det nya tillgängliga innehållet. När detta inträffar kan vissa mediaegenskaper ändras.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Nytt i 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> When a media player item is updated. För live/linjär direktuppspelning måste klienten regelbundet uppdatera medieresursen för att kunna identifiera det nya tillgängliga innehållet. När detta inträffar kan vissa mediaegenskaper ändras.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Nytt i 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> When a media player item is updated. För live/linjär direktuppspelning måste klienten regelbundet uppdatera medieresursen för att kunna identifiera det nya tillgängliga innehållet. När detta inträffar kan vissa mediaegenskaper ändras.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Nytt i 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> som skickas när tidsinställda händelser genereras.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>Nytt i 2.0</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>gränssnitt ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>gränssnitt ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> attribute double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TextFormat {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td>Ingen ändring för 2.0</td> 
   <td><p>interface TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DARK_GREEN = 8 ;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10;<br /> const unsigned short COLOR_DARK_BLUE = 11;<br /> const unsigned short COLOR_BLUE = 12;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14;<br /> const unsigned short COLOR_YELLOW = 15;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16;<br /> const unsigned short COLOR_DARK_MAGENTA = 17;<br /> const unsigned short COLOR_MAGENTA = 18;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19;<br /> const unsigned short COLOR_DARK_CYAN = 20;<br /> const unsigned short COLOR_CYAN = 21;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22;<br /> <br /> skrivskyddat attribut unsigned short fontColor;<br /> skrivskyddat attribut unsigned short backgroundColor;<br /> skrivskyddat attribut unsigned short fillColor;<br /> skrivskyddat attribut unsigned short edgeColor;<br /> <br /> // Size<br /> const unsigned short SIZE_DEFAULT = 0;<br /> const unsigned short SIZE_SMALL = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> const unsigned short SIZE_LARGE = 3 ;<br /> <br /> skrivskyddat attribut med kort storlek utan tecken,<br /> <br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2 ;<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> skrivskyddat attribut unsigned short fontEdge;<br /> <br /> // Font<br /> const unsigned short FONT_DEFAULT = 0;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const unsigned short FONT_SMALL_CAPITALS = 6 ;<br /> skrivskyddat attribut med kort teckensnitt utan tecken,<br /> skrivskyddat attribut osignerat kort fontOpacity;<br /> skrivskyddat attribut osignerad kort bakgrundOpacitet,<br /> skrivskyddat attribut unsigned short fillOpacity;<br /> skrivskyddat attribut osignerat kort DEFAULT_OPACITY;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource resource, long resourceId,<br /> ItemLoaderListener listener, <br /> MediaPlayerItemConfig config);<br /> void cancel();<br /> skrivskyddat attribut MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Nytt i 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>Nytt i 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Ändringar i API-elementet för mediaegenskaper för 2.0 {#media-characteristics-api-element-changes-for}

I de här tabellerna jämförs API-elementen för medieegenskapen för C++ TVSDK mellan version 1.3 och 2.0.

Tabeller i det här avsnittet:

* MediaPlayerItem
* Track, AudioTrack, ClosedCaptionsTrack
* Profil
* DRMMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItem {<br /> readonly attribute MediaResource;<br /> skrivskyddat attribut long resourceId;<br /> skrivskyddat attribut boolesk live,<br /> <br /> skrivskyddat attribut booleskt hasAlternateAudio;<br /> skrivskyddat attribut AudioTrackList audioTracks;<br /> skrivskyddat attribut AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(ljudspår); <br /> <br /> skrivskyddat attribut booleskt hasClosedCaptions;<br /> skrivskyddat attribut ClosedCaptionsTrackList closedCaptionsTracks;<br /> skrivskyddat attribut ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> spårningen ClosedCaptionsTrack); <br /> <br /> skrivskyddat attribut boolean hasTimedMetadata;<br /> skrivskyddat attribut TimedMetadataList timedMetadata;<br /> skrivskyddat attribut booleskt dynamiskt,<br /> <br /> skrivskyddat attribut boolean isProtected;<br /> skrivskyddat attribut DRMMetadataInfoList drmMetadataInfos;<br /> skrivskyddade attribut ProfileList-profiler;<br /> skrivskyddad attributprofil selectedProfile;<br /> <br /> skrivskyddat attribut boolean trickPlaySupported;<br /> skrivskyddat attribut FloatArray availablePlaybackRates;<br /> skrivskyddat attribut float selectedPlaybackRate;<br /> <br /> <br /> skrivskyddat attribut MediaPlayer mediaPlayer;<br /> skrivskyddat attribut, konfiguration av MediaPlayerItemConfig;<br /> };</p> </td> 
   <td><p>interface MediaPlayerItem {<br /> readonly attribute MediaResource;<br /> skrivskyddat attribut long resourceId;<br /> skrivskyddat attribut boolesk live,<br /> <br /> skrivskyddat attribut booleskt hasAlternateAudio;<br /> skrivskyddat attribut AudioTrackList audioTracks;<br /> attribute AudioTrack selectedAudioTrack;<br /> <br /> <br /> skrivskyddat attribut booleskt hasClosedCaptions;<br /> skrivskyddat attribut ClosedCaptionsTrackList ccTracks;<br /> attribute ClosedCaptionsTrack selectedCCTrack;<br /> <br /> <br /> <br /> skrivskyddat attribut boolean hasTimedMetadata;<br /> skrivskyddat attribut TimedMetadataList timedMetadata;<br /> skrivskyddat attribut booleskt dynamiskt,<br /> <br /> skrivskyddat attribut boolean isProtected;<br /> skrivskyddat attribut DRMMetadataInfoList drmMetadataInfos;<br /> skrivskyddade attribut ProfileList-profiler;<br /> <br /> <br /> skrivskyddat attribut boolean trickPlaySupported;<br /> skrivskyddat attribut Int32Array availablePlaybackRates;<br /> <br /> skrivskyddat attribut StringList adTags;<br /> <br /> skrivskyddat attribut MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Track / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br /> readonly attribute DomString name;<br /> skrivskyddat attribut DOMString-språk;<br /> boolesk standardinställning för skrivskyddat attribut,<br /> skrivskyddat attribut boolean autoSelect;<br /> }; </p> </td> 
   <td>Nytt i 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack : Spåra<br /> {<br /> readonly attribute DomString name;; //FromTrack<br /> readonly attribute DOMString language;//FromTrack<br /> readonly attribute boolean default; // From Track<br /> readonly attribute boolean autoSelect;//FromTrack<br /> <br /> readonly attribute unsigned int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> readonly attribute DomString name;<br /> skrivskyddat attribut DOMString-språk; <br /> boolesk standardinställning för skrivskyddat attribut,<br /> skrivskyddat attribut boolean autoSelect;<br /> skrivskyddat attribut (booleskt) framtvingat,<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Ingen ändring för 2.0</td> 
   <td><p>interface AudioTrackList<br /> {<br /> readonly attribute unsigned long length;<br /> getter AudioTrack (unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack : Spåra<br /> {<br /> readonly attribute DomString name;; //FromTrack<br /> readonly attribute DOMString language;//FromTrack<br /> readonly attribute boolean default; // FromTrack<br /> readonly attribute boolean autoSelect;//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> skrivskyddat attribut unsigned short serviceType;<br /> skrivskyddat attribut (booleskt) framtvingat,<br /> };</p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> readonly attribute DomString name;<br /> skrivskyddat attribut DOMString-språk;<br /> boolesk standardinställning för skrivskyddat attribut,<br /> <br /> <br /> boolesk skrivskyddad attribut är aktivt,<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Ingen ändring för 2.0</td> 
   <td><p>interface ClosedCaptionsTrackList<br /> {<br /> readonly attribute unsigned long;<br /> getter ClosedCaptionsTrack(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Profil {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td>Profil: Ingen ändring för 2.0</td> 
   <td><p>gränssnittsprofil<br /> {<br /> readonly attribute unsigned int width;<br /> skrivskyddat attribut osignerad int-höjd,<br /> skrivskyddat attribut osignerat int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>Profillista: Ingen ändring för 2.0</td> 
   <td><p>interface ProfileList<br /> {<br /> readonly attribute unsigned long;<br /> getter Profile(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>: Ingen ändring för 2.0</td> 
   <td><p>gränssnitt för DRMMetadataInfo<br /> { <br /> skrivskyddade DRMMetadata-metadata;<br /> skrivskyddat attribut long prefetchTimestamp;<br /> skrivskyddat attribut TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Ingen ändring för 2.0</td> 
   <td><p>gränssnittet DRMMetadataInfoList<br /> {<br /> skrivskyddat attribut med lång längd utan tecken;<br /> getter DRMMetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Mappa C++-fel till undantag på olika språk {#mapping-c-errors-to-exceptions-in-different-languages}

Du kan mappa C++-felkoder till undantag på olika språk.

C++ PSDK har en no throw-princip för sina API:er. De flesta API-metoderna returnerar ett PSDKErrorCode-värde som anger om metoden kördes korrekt. Asynkrona fel meddelas via felhändelser.

ActionScript och JAVA PSDK har en annan policy. De flesta felen genererar ett ArgumentError eller IllegalStateException som anger att den synkrona delen av metoden inte kunde köras. Dessa undantag fångas inte upp och programkoden ansvarar för att hantera undantagen. De innehåller vanligtvis användbar information om varför metodanropet misslyckades. Om till exempel kommandot prepareToPlay anropas i ett ogiltigt läge genereras följande undantag:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

ActionScript/JAVA genererar också undantag från konstruktorer för att ange att vissa interna objekt skapades felaktigt. Dessa undantag hanteras internt och sprids inte till programmet. Undantagen inkluderas i ett varningsmeddelande som skickas till programmet

Om t.ex. ingen giltig mediefil hittades för det mottagna annonssvaret kan inget giltigt annonsobjekt eller -annons skapas. Därför placeras ingen annons på tidslinjen och ett NotificationEvent.OperationFailed-meddelande skickas.

Fel- eller varningskoder som tas emot asynkront från Adobe Video Engine (AVE) skickas till programmet som vanliga händelser. Meddelandehändelsen innehåller alla mottagna felkoder och eventuella ytterligare metadata, t.ex. URL:en, resursidentifieraren, handtag o.s.v. Om felet är allvarligt och uppspelningen av det aktuella mediet inte kan fortsätta, övergår MediaPlayer till ERROR-status och onStatusChanged-återanropet eller MediaPlayerStatusChanged.STATUS_CHANGED-händelsen skickas. Om uppspelningen kan fortsätta skickas en normal meddelandehändelse.

<table> 
 <tbody> 
  <tr> 
   <th>C++-fel (PSDKError-kod)</th> 
   <th> </th> 
   <th>Java</th> 
   <th>ActionScript</th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Undantag med koden = 1, description = "INVALID_ARGUMENT" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Undantag med koden = 2, description = "GENERIC_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>Undantag med kod = 3, description = "ILLEGAL_STATE" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 4, description = "GENERIC_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med koden = 5, description = "CREATION_FAILED" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kecunsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med koden = 5, description = "CREATION_FAILED" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 7, description = "DATA_NOT_AVAILABLE" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 8, description = "SEEK_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kecunsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med koden = 9, description = "UNSUPPORTED_FEATURE" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kRecangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med koden = 10, description = "RANGE_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 11, beskrivning = "CODEC_NOT_SUPPORTED" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 12, description = "MEDIA_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 13, description = "NETWORK_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error eller MediaPlayerNotification.Warning</td> 
   <td>MediaError eller NotificationEvent</td> 
   <td>Undantag med koden = 14, description = "GENERIC_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 15, description = "INVALID_SEEK_TIME" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 16, description = "AUDIO_TRACK_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 17, description = "GENERIC_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med koden = 18, description = "GENERIC_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med kod = 19, description = "GENERIC_ERROR" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Undantag med koden = 200, description = "PLAYBACK_OPERATION_FAILED" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Undantag med kod = 201, description = "NATIVE_WARNING" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Undantag med koden = 202, description = "AD_RESOLVER_FAILED" och additionalInfo= &lt;som skickas av metoden som utlöste det här undantaget&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Elementändringar i Utility och Helper API för 2.0 {#utility-and-helper-api-element-changes-for}

I dessa tabeller jämförs Utility- och Helper API-elementen för JavaScript TVSDK mellan version 1.3 och 2.0.

Tabeller i det här avsnittet:

* Version
* TimeRange
* QOSProvider
* DeviceInformation
* LoadInfo
* Visa
* PlaybackInformation

### Version {#version}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface Version<br /> {<br /> readonly attribute DomString version;<br /> skrivskyddat attribut DOMString-beskrivning;<br /> skrivskyddat attribut för long major,<br /> skrivskyddat attribut long minor,<br /> skrivskyddat attribut för lång revision,<br /> skrivskyddat attribut long apiVersion;<br /> };</p> </td> 
   <td><p>interface Version<br /> {<br /> readonly attribute DomString version;<br /> skrivskyddat attribut DOMString-beskrivning;<br /> skrivskyddat attribut DomString major;<br /> skrivskyddat attribut DomString minor;<br /> skrivskyddat attribut DomString-revision;<br /> skrivskyddat attribut DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimeRange {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td>Ingen ändring för 2.0</td> 
   <td><p>interface TimeRange<br /> {<br /> readonly attribute unsigned long begin;<br /> skrivskyddat attribut utan signerad lång ände,<br /> skrivskyddat attribut med osignerad lång varaktighet,<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td>Ingen ändring för 2.0</td> 
   <td><p>gränssnittet QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> skrivskyddat attribut DeviceInformation deviceInformation;<br /> skrivskyddat attribut PlaybackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DeviceInformation {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>gränssnittet DeviceInformation<br /> {<br /> readonly attribute DomString os;<br /> <br /> <br /> <br /> skrivskyddat attribut DomString id;<br /> skrivskyddat attribut int sityDPI;<br /> skrivskyddat attribut int heightPixels;<br /> skrivskyddat attribut int widthPixels;<br /> skrivskyddat attribut booleskt seekToKeyFrame;<br /> };</p> </td> 
   <td><p>gränssnittet DeviceInformation<br /> {<br /> readonly attribute DomString os;<br /> skrivskyddat attribut int sdk,<br /> skrivskyddat attribut DOMString-modell;<br /> skrivskyddat attribut DOMString-tillverkare;<br /> skrivskyddat attribut DomString id;<br /> skrivskyddat attribut int sityDPI;<br /> skrivskyddat attribut int heightPixels;<br /> skrivskyddat attribut int widthPixels;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td>Ingen ändring för 2.0</td> 
   <td><p>interface LoadInfo<br /> {<br /> readonly attribute DomString url;<br /> skrivskyddat attribut i int-storlek,<br /> skrivskyddat attribut double downloadDuration;<br /> skrivskyddat attribut int periodIndex;<br /> skrivskyddat attribut double mediaDuration;<br /> skrivskyddat attribut short TRACK_TYPE_FRAGMENT;<br /> skrivskyddat attribut short TRACK_TYPE_TRACK;<br /> skrivskyddat attribut short TRACK_TYPE_MANIFEST;<br /> skrivskyddad attributkort typ,<br /> skrivskyddat attribut DomString trackName;<br /> skrivskyddat attribut DOMString trackType;<br /> skrivskyddat attribut int trackIndex,<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Visa {#view}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td>Ingen ändring för 2.0</td> 
   <td><p>interface View<br /> {<br /> readonly attribute unsigned short x;<br /> skrivskyddat attribut unsigned short y,<br /> skrivskyddat attribut med kort bredd utan tecken,<br /> skrivskyddat attribut med kort höjd utan tecken,<br /> <br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### PlaybackInformation {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API:er</th> 
   <th>1.3 API:er</th> 
  </tr> 
  <tr> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attribute double timeToFirstByte;<br /> skrivskyddat attribut double timeToLoad;<br /> skrivskyddat attribut double timeToStart;<br /> skrivskyddat attribut double timeToFail;<br /> skrivskyddat attribut int totalSecondsPlayed;<br /> skrivskyddat attribut int totalSecondsSpent;<br /> skrivskyddat attribut double frameRate;<br /> skrivskyddat attribut int droppedFrameCount;<br /> skrivskyddat attribut int percepeivedBandwidth;<br /> skrivskyddat attribut, int-bithastighet,<br /> skrivskyddat attribut double bufferTime;<br /> skrivskyddat attribut int bufferLength;<br /> skrivskyddat attribut int emptyBufferCount;<br /> skrivskyddat attribut double bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attribute double timeToFirstByte;<br /> skrivskyddat attribut double timeToLoad;<br /> skrivskyddat attribut double timeToStart;<br /> skrivskyddat attribut double timeToFail;<br /> skrivskyddat attribut int totalSecondsPlayed;<br /> skrivskyddat attribut int totalSecondsSpent;<br /> skrivskyddat attribut double frameRate;<br /> skrivskyddat attribut int droppedFrameCount;<br /> <br /> skrivskyddat attribut, int-bithastighet,<br /> skrivskyddat attribut double bufferTime;<br /> skrivskyddat attribut int bufferLength;<br /> skrivskyddat attribut int emptyBufferCount;<br /> skrivskyddat attribut double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Användbara resurser {#helpful-resources}

* Fullständig hjälpdokumentation finns på [Adobe Primetime sida för utbildning och support](https://helpx.adobe.com/support/primetime.html) .
