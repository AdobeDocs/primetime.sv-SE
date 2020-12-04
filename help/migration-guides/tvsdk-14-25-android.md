---
title: TVSDK 1.4 till 2.5 för Android (Java)
seo-title: TVSDK 1.4 till 2.5 för Android (Java)
description: TVSDK 2.5 har många fördelar jämfört med version 1.4 när det gäller prestanda, säkerhet, bättre integrering och mycket annat.
seo-description: TVSDK 2.5 har många fördelar jämfört med version 1.4 när det gäller prestanda, säkerhet, bättre integrering och mycket annat.
uuid: aaab7aec-cb5b-4840-82e8-7112a8d98a8a
contentOwner: vishgupt
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: 8d9136bf-b3ae-450c-bd8a-0bb246527886
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '2343'
ht-degree: 0%

---


# TVSDK 1.4 till 2.5 för Android (Java) {#tvsdk-to-for-android-java}

TVSDK 2.5 har många fördelar jämfört med version 1.4 när det gäller prestanda, säkerhet, bättre integrering och mycket annat.

TVSDK löser de största utmaningarna på den enhet som betyder mest. Android fortsätter att vara den globala dominansen, med över 86 % av marknadsandelen. Migrering till TVSDK på Android optimerar uppspelningsprestanda för att öka användarengagemanget och snabba upp time-to-market med stöd för nya innehållsformat.

## Fördelar med att migrera till TVSDK v2.5 {#benefits-of-migrating-to-tvsdk-v}

TVSDK 2.5 har många fördelar jämfört med version 1.4 när det gäller prestanda, säkerhet, bättre integrering och mycket annat. Läs vidare för att snabbt få reda på fördelarna med att migrera till den nya versionen.

Enligt en jämförande studie från tredje part ger v2.5 en 5 gånger kortare starttid och 3,8 gånger kortare uteslutna bildrutor jämfört med branschens genomsnitt.

| Prestandafunktioner | Beskrivning |
|--- |--- |
| Direkt för VOD och Live | Läs in inledande segment i förväg för omedelbar uppspelning av VOD och direktlinjär direktuppspelning när kanalväxling används, för en TV-liknande upplevelse. |
| Lazy och laddning | Startar uppspelningen så snart förrullning eller innehåll är tillgängligt och löser annonser i mellanrullning i en parallelltråd. |
| Beständiga nätverksanslutningar | Öka effektiviteten och minska fördröjningen i nätverkskoden för snabbare uppspelningsprestanda. |
| Förbättrad ABR-logik | Den nya ABR-logiken baseras på buffertlängd, förändringshastighet för buffertlängd och uppmätt bandbredd. Detta garanterar att ABR väljer rätt bithastighet när bandbredden ändras och även optimerar antalet gånger som bithastighetsväxlingen faktiskt sker genom att övervaka den hastighet med vilken buffertlängden ändras. |
| Nedladdning av delar av segment | Startar uppspelningen så snart det finns tillräckligt med bildrutor från ett segment för att återge video på klientsidan. |
| Parallella nedladdningar | TVSDK hämtar ljud- och videosegment parallellt för demultiplexat innehåll för att optimera uppspelningsprestanda. |

Uppspelningsfunktionerna förbättrar konsumenternas engagemang genom att leverera upplevelsen av linjär sändning i digitalt format. Det hjälper dig också att utnyttja inbyggt DRM, t.ex. Widewin för HD-uppspelning.

| Uppspelningsfunktioner | Beskrivning |
|--- |--- |
| MP4-uppspelning | Korta MP4-klipp behöver inte omkodas för att spelas upp i TVSDK. |
| Uppspelning av VOD-innehåll i DASH | Grundläggande VOD-uppspelningsexempel för DASH stöds. |
| Smooth Trickplay med ABR | Stöd för snabb framåtspolning och tillbakaspolning i HLS med nyckelrutor med låg hastighet och I-Frames med snabbare hastighet. ABR-stöd för alla bildrutor som stöds. |

Funktionerna är viktiga för att uppfylla studiobegränsningarna, som HD-uppspelning över DRM.

| Funktioner | Beskrivning |
|--- |--- |
| Upplösningsbaserat utdataskydd | uppspelningen kan begränsas till endast vissa upplösningar som tillåts av DRM-krav. Endast tillgängligt via Primetime DRM. |
| Stöd för fler | Stöds med DASH VOD-strömmar för att aktivera interna DRM-användningsfall. |

Direktfakturering eliminerar behovet av att skapa manuella rapporter för fakturering varje månad. VHL 2.0 ger kortare time-to-market med integrering före bygget och bättre noggrannhet i spårningen.

| Funktioner | Beskrivning |
|--- |--- |
| Moat-integrering | Stöd för visning av annonser från Moat. |
| VHL 2.0 | Den senaste optimerade videofilmen fångar biblioteksintegrationen för automatisk insamling av användningsdata för Adobe Analytics. |
| Stöd för failover | Ytterligare strategier har implementerats för att fortsätta oavbruten uppspelning, trots fel på värdservrar, spellistfiler och segment. |
| Direkt faktureringsintegrering | Faktureringsstatistik skickas till Adobe Analytics backend, som certifieras av Adobe Primetime för strömmar som används av kunden. |

>[!NOTE]
>
>Alla funktioner i TVSDK v1.4 stöds i v2.5, förutom Multi-CDN-stöd.

## Översikt över migreringsprocessen {#overview-of-the-migration-process}

Att smidigt migrera från TVSDK 1.4 till 2.5 innebär att man måste byta till version 2.5-bibliotek, kompilera om och sedan använda det här dokumentet för att felsöka eventuella problem som inträffar.

TVSDK v1.4-bibliotek fungerar inte med och samexisterar inte med v2.5-bibliotek. Du måste använda v2.5-bibliotek med TVSDK 2.5 och migrera dina program och integreringar för att uppgradera till TVSDK 2.5. I det här dokumentet beskrivs hur och vad du ska ändra i programkoden och hur du åtgärdar fel under omkompileringen.

Filen psdk.jar använder bibliotek från tredje part för att stödja olika funktioner. Ta med följande i `proguard.cfg`-filen för att förhindra att biblioteken tas bort:

```java
# Adobe TVSDK keep classes
-keep class com.adobe.** { *; }
-keep class com.google.android.exoplayer.**
{ *; }
```

I `build.gradle`-filen måste du ta med kompileringsdirektivet för att inkludera TVSDK-baserade JAR-filer. Om appen innehåller Adobe Video Analytics måste du ta med kompileringsdirektivet för de ytterligare burar som krävs för Adobe Video Analytics-integrering i appen

```java
# Compile Adobe TVSDK jars compile files('libs/psdk-va.jar')
compile files('libs/VideoHeartbeat.jar')
```

Flera mindre ändringar ingår inte i det här dokumentet. Om du vill se mindre ändringar i API:t läser du [TVSDK 2.5 för Android Java API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/index.html). Motsvarande API-referens för C++ har detaljerade beskrivningar. Analog API-dokumentation för C++ finns i [TVSDK 2.5 för Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.5/index.html).

Flera exempel på API-användning beskrivs i referensimplementeringen som distribueras med TVSDK.

## API-ändringar i TVSDK v2.5 {#api-changes-in-tvsdk-v}

De nya, föråldrade och ändrade API:erna beskrivs nedan.

| TVSDK v1.4 | TVSDK v2.5 | Beskrivning |
|--- |--- |--- |
| import com.adobe.ave.drm.DRMAcquireLicenseSettings | import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; | Alla klassnamn i TVSDK 2.5 API börjar med prefixet com.adobe.mediacore. Detta är bara ett exempel. |
| MediaPlayerException, IllegalStateException eller IllegalArgumentException | MediaPlayerException | I 2.5 genererar API:erna endast MediaPlayerException. |
| MediaPlayer.PlayerState (MediaPlayer.Event.PLAYBACK) | MediaPlayerStatus (MediaPlayerEvent.STATUS_CHANGED) | I v2.5 har namnet på MediaPlayer.PlayerState ändrats till en separat uppräkning av MediaPlayerStatus. |
| DefaultMediaPlayer.create (getActivity().getApplicationContext()) | MediaPlayer mediaPlayer = new MediaPlayer(getActivity()). getApplicationContext()); | De statiska metoder som används för att skapa objekt ersätts av offentliga konstruktorer. |
| MediaPlayer.seekToLocalTime() | MediaPlayer.seekToLocal() | Metoden MediaPlayer.seekToLocalTime() kallas nu MediaPlayer.seekToLocal(). |
| closedCaptionsTrack.isActive() |  | Inte tillgängligt |
| MetadataNode | Metadata | I v2.5 ersätter klassen Metadata användningen av klassen v1.4 MetadataNode. |
| DefaultMetadataKeys | MetadataKeys | DefaultMetadataKeys från v1.4 finns i v2.5 enum MetadataKeys. |
| AdvertisingFactory | ContentFactory | AdvertisingFactory från v1.4 har bytt namn till ContentFactory i v2.5 |
| PlacementOpportunityDetector | OpportunityGenerator | Detektorer ersätts med generatorer. |
| mediaPlayer.getView().notifyClick(); | mediaPlayer.notifyClick(); | Metoden notifyClick() i MediaPlayerView har flyttats till klassen MediaPlayer. |
| public ABRControlParameters(ABRPolicy abrPolicy, int nInitialBitRate, int nMinBitRate, intMaxBitRate) | public ABRControlParameters(int InitialBitRate, int nMinBitRate, int nMaxBitRate, ABRPolicy abrPolicy, int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate, int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate) |  |
| playbackInformation.getTimeToFirstFrame() |  | Inte tillgängligt |
|  | playbackInformation.get PerceivedBandwidth() | TVSDK v2.5 QOSProvider har en ny egenskap som avgör den upplevda bandbredden under en direktuppspelningssession. |

### Borttagna klasser {#removed-classes}

Följande klasser tas bort och har inga motsvarigheter.

* `TimeRangeCollection`
* `PSDKConfig`
* `BaseLogger`
* `DefaultLogger`
* `Log`
* `Logger`
* `LogFactory`
* `NullLogger`

De sista sex av dessa klasser är tillgängliga som hjälpklasser i referensimplementeringen.

## Namnområdesändringar {#namespace-changes}

API:t TVSDK 2.5 konsoliderar namnutrymmen.

Alla klassnamn i TVSDK 2.5 API börjar med prefixet com.adobe.mediacore. Vissa klassnamn i TVSDK 1.4 API börjar med com.adobe.ave. Motsvarande 2.5-klasser ändrar com.adobe.ave till com.adobe.mediacore. Observera t.ex. ändringarna i följande kodrader för 1.4 och 2.5:

```java
// TVSDK 1.4
import com.adobe.ave.drm.DRMAcquireLicenseSettings; import com.adobe.ave.drm.DRMLicense;
import com.adobe.ave.drm.DRMManager; import com.adobe.ave.drm.DRMMetadata
```

```java
// TVSDK 2.5
import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; import com.adobe.mediacore.drm.DRMLicense;
import com.adobe.mediacore.drm.DRMManager; import com.adobe.mediacore.drm.DRMMetadata;
```

## Ändringar i händelsehantering {#changes-in-event-handling}

Om du vill registrera händelser i den här versionen skickar du hanteraren till `addEventListener`. Förteckningen över händelser har ändrats väsentligt från version 1.4 till version 2.5.\
Här beskrivs till exempel hur du registrerar en händelsehanterare för `MediaPlayerEvent.STATUS_CHANGED:`

```java
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,
new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
});
```

Så här registrerades händelsen i 1.4:

```java
mPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {
@Override
public void onStateChanged(MediaPlayer.PlayerState state,
MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});
```

Uppräkningen MediaPlayerEvent innehåller alla händelsekoder. Följande händelsekoder från 1.4 finns inte längre i 2.5:

* `ADBREAK_PLACEMENT_COMPLETED`
* `ADBREAK_PLACEMENT_FAILED`
* `ADBREAK_REMOVAL_COMPLETED`
* `AD_BREAK_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_FAILED`
* `AUDIO_TRACK_FAILED`
* `BACKGROUND_MANIFEST_FAILED`
* `BUFFERING_FULL, CUSTOM_AD_EVENT`
* `CONTENT_MARKER`
* `CONTENT_PLACEMENT_COMPLETE`
* `CONTENT_CHANGED`
* `ITEM_REPLACED`
* `ITEM_READY`
* `VIEW_CLICKED`
* `PREPARED`
* `UPDATED`
* `OPPORTUNITY_COMPLETED`
* `OPPORTUNITY_CREATED`
* `OPPORTUNITY_FAILED`
* `PAUSE_AT_PERIOD_END`
* `PLAYBACK_STARTED`
* `PLAYBACK_PAUSED`
* `PLAYBACK_COMPLETED`
* `PLAY_COMPLETE`
* `POST_ROLL_COMPLETE`
* `RESOURCE_LOADED`
* `TIMED_METADATA_SKIPPED`
* `VIDEO_ERROR`
* `VIDEO_STATE_CHANGED`

Följande händelsekoder är nya i 2.5:

* `AD_RESOLUTION_COMPLETE`
* `BUFFER_PREPARED`
* `CAPTIONS_UPDATED`
* `MANIFEST_UPDATED`
* `PLAYBACK_RANGE_UPDATED`
* `RESERVATION_REACHED`
* `TIME_CHANGED`
* `TIMED_EVENT`
* `TIMED_METADATA_ADDED_IN_BACKGROUND`

### Bytt namn på händelser {#renamed-events}

| Nytt namn | Gammalt namn |
|--- |--- |
| SEEK_BEGIN | SEEK_STARTED |
| SEEK_END | SEEK_COMPLETED |
| SEEK_POSITION_ADJUSTED | SEEK_ADJUST_COMPLETED |
| BUFFERING_BEGIN | BUFFERING_STARTED |
| BUFFERING_END | BUFFERING_COMPLETED |
| AUDIO_TRACK_UPDATED | AUDIO_TRACK_CHANGED |
| STATUS_CHANGED | STATE_CHANGED |
| TIMED_METADATA_AVAILABLE | TIMED_METADATA_ADDED |
| SIZE_AVAILABLE | SIZE_CHANGED |
| LOAD_INFO | LOAD_INFORMATION_AVAILABLE |

## Ändringar i MediaPlayer {#mediaplayer-changes}

Ett nytt sätt att konstruera `MediaPlayer` och ändra vissa metoder.

**Ändringar i klassen MediaPlayer**

Här är ändringarna av klassen `MediaPlayer`:

* Uppräkningen `MediaPlayerStatus` ersätter `MediaPlayer.PlayerState`. Exempel:

```java
//TVSDK v1.4
mPlayer. addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {

@Override
public void onStateChanged(MediaPlayer.PlayerState state,MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});

//TVSDK v2.5
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
//Additional handlers.
...
});
```

* Metoden `MediaPlayer.seekToLocalTime()` kallas nu `MediaPlayer.seekToLocal`. Exempel:

```java
//TVSDK v1.4
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocalTime(localPosition);
}

//TVSDK v2.5
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocal(localPosition);
}
```

* Metoden `MediaPlayerView.notifyClick()` är nu `MediaPlayer.notifyClick()`. Exempel:

```java
//TVSDK v1.4
public void adClick() { mediaPlayer.getView().notifyClick();
}

//TVSDK v2.5
public void adClick() { mediaPlayer.notifyClick();
}
```

* Den tidigare `MediaPlayer.MediaPlayer.getNotificationHistory()`-metoden är nu borta och ersätts inte.
* Den första `MediaPlayer.replaceCurrentItem()` delas upp i två metoder: `replaceCurrentResource()`, som tar en instans av `MediaResource` och `replaceCurrentItem()`, som tar en instans av `MediaPlayerItem`. Exempel:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());

mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5 - replacing a resource
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());
...
try {
mMediaPlayer.replaceCurrentResource(playerResource, _mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
// TVSDK 2.5 - replacing an Item
MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(context, new MediaPlayerItemLoader.LoaderListener() {

@Override
public void onError(PSDKErrorCode psdkErrorCode, String s) {
...
}
@Override
public void onLoadComplete(MediaPlayerItem mediaPlayerItem) {
...
}
@Override
public void onBufferingBegin() {
...
}
@Override
public void onBufferPrepared() {
...
}
});
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());

itemLoader.load(playerResource); itemLoader.prepareBuffer();
mediaPlayer.replaceCurrentItem(itemLoader.getItem());
```

Du kan använda den här metoden för att växla mellan förinitierade MediaPlayer-instanser, som vid utfall.

**Konstruktorer ersätter statiska create()-metoder**

Du kan använda konstruktorer i TVSDK v2.5 i stället för att använda metoderna `create()` för TVSDK v1.4. Alla klasser med namn som börjar med Standard, som `DefaultMediaPlayer`, `DefaultNetworkConfig`, `DefaultContentFactory`, är inte tillgängliga i v2.5.

I vissa fall använder TVSDK v1.4 API följande mönster för att skapa klasser:

1. Definiera ett gränssnitt (till exempel `MediaPlayer`).
1. Ange en standardklass (till exempel `DefaultMediaPlayer`).
1. Ange en `create()`-metod i standardklassen för att tillhandahålla en klass som implementerar gränssnittet.

I TVSDK v2.5 är sådana gränssnitt konkreta klasser och du skapar instanser av dessa klasser med respektive konstruktor. Följande kodfragment visar den här skillnaden:

```java
//TVSDK v1.4
// Create a media player
// MediaPlayer is an interface
private MediaPlayer createMediaPlayer() { MediaPlayer mediaPlayer =
DefaultMediaPlayer.create(getActivity().getApplicationContext()); return mediaPlayer;

//TVSDK v2.5
// Create a media player
// MediaPlayer is a class that you instantiate private MediaPlayer createMediaPlayer() {
MediaPlayer mediaPlayer =
new MediaPlayer(getActivity().getApplicationContext()); return mediaPlayer;
}
```

Andra klasser som inte följer mönstret men använder `create()`-metoder i 1.4 är:

* MediaResource\
   Detta användes tidigare `MediaResource.createFromUrl()`. Använd nu konstruktorn som tar en URL, resurstyp och metadata. Exempel:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());
mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, getAdvertisingMetadata());

try { mediaPlayer.replaceCurrentResource(playerResource,_mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
```

* Annons
* AdAsset
* AdBreak

Vissa klasser (till exempel `ContentFactory`) är abstrakta klasser utan offentligt tillgänglig standardimplementering (till exempel `DefaultContentFactory`). I dessa fall kan du tillhandahålla en standardimplementering via en praktisk funktion, till exempel: `mediaPlayerItemConfig.getDefaultContentFactory()`

**Förändringar i undertexter**

Följande ändringar påverkar klasser för undertextning:

* När du hämtar spår för undertexter returnerar `MediaPlayerItem.getClosedCaptionTracks()` bara aktiva spår.
* `ClosedCaptionTrack` har inte längre någon  `isActive()` metod.

```java
//TVSDK v1.4
public List<String> getClosedCaptionTracks(String label) {
List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks(); Iterator<ClosedCaptionsTrack> iterator =
closedCaptionsTracks.iterator();
if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); String isActive = closedCaptionsTrack.isActive() ? " (" + label
+ ")" : "";
closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName()
+ " : " + closedCaptionsTrack.getLanguage() + isActive);
}
}
return closedCaptionsTracksAsStrings;
}

//TVSDK v2.5
public List<String> getClosedCaptionTracks(String label) {

MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks();
Iterator<ClosedCaptionsTrack> iterator = closedCaptionsTracks.iterator();

List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); closedCaptionsTracksAsStrings.
add(closedCaptionsTrack.getName() + " : ");
}
}
return closedCaptionsTracksAsStrings;
}
// Add snippet and desc for CaptionsUpdatedEventListener mediaPlayer.addEventListener(MediaPlayerEvent.CAPTIONS_UPDATED,
captionsUpdatedEventListener);

private final CaptionsUpdatedEventListener captionsUpdatedEventListener = new CaptionsUpdatedEventListener() {

@Override
public void onCaptionsUpdated(MediaPlayerItemEvent mediaPlayerItemEvent) { getActivity().findViewById(R.id.sbPlayerControlCC).setVisibility(
View.VISIBLE/*Visible*/);
}
};
```

## Reklamändringar {#advertising-changes}

Det finns flera annonsrelaterade ändringar i version 2.5.

**Förändringar i reklambeteendet**

Standardbeteendet för annonsuppspelningen när en användare utför en sökning utanför en Ad-ruta ändras något i v2.5. Om annonsbrytningen inte bevakas spelas annonsen upp efter en sökning framåt. När appen använder standardannonsprincipen tas annonsbrytningen bort när uppspelningen är klar. Om en användare använder TVSDK v2.5 och söker bakom en annonsruta på tidslinjen och annonsbrytningen inte bevakas, spelas ingen annons upp.

I TVSDK v1.4 spelas en annons upp som standard om sökningen görs bakåt. Om du till exempel söker bakåt mellan den tredje och fjärde annonsbrytningen är standardbeteendet för TVSDK v1.4 att spela upp den tredje annonsbrytningen.

**Ändring av annonsregler**

Annonsreglerna anges med en JSON-fil. JSON-filens format ändras inte i båda versionerna av TVSDK. I TVSDK v2.5 måste dock JSON-filen för annonsregler finnas på en plats som är tillgänglig via en HTTP-URL. Programmet kan använda en instans av AuditudeSettings.

```java
//TVSDK v2.5
AuditudeSettings result = new AuditudeSettings(); result.setCRSRulesJsonURL(<http url of AdobeTVSDKConfig.json>);
```

I TVSDK version 1.4 placeras den här filen under mappen assets i programmet och TVSDK läser in filen.

**Annonsfabriksbyte**

`AdvertisingFactory` har fått sitt namn  `ContentFactory`. Med `ContentFactory` kan du skapa anpassade arbetsflöden för annonsering genom att åsidosätta några av dess metoder. Använd return null för att behålla standardbeteendena, som i följande:

```java
//TVSDK v2.5
new ContentFactory() {
@Override
public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item) { return new CustomAdPolicySelector();
}
@Override
public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { return null;
}
@Override
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { return null;
}
@Override
public List<CustomAdHandler> retrieveCustomAdPlaybackHandlers(MediaPlayerItem item) { return null;
}
};
```

**Nollängd - annonsbrytningar**

TVSDK 2.5 infogar annonsbrytningar med nollängd som platshållare när annonsservern inte returnerar några annonser.

Nolllängden på annonsbrytningar kan bestämmas genom att antalet annonser som är noll i annonseringsbrytningen identifieras med händelsen onAdBreakStarted och programmet måste hantera annonsuppbrytningarna därefter.

**Metadataändringar**

Metadataklassen ger en bättre funktion för den tidigare klassen MetadataNode.

* Metadataklassen kan lagra strängar, bytearrayer och andra metadataobjekt:

```java
TVSDK v1.4
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new MetadataNode();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingParameters(advertisingParams);

return adSettings;
}
//TVSDK v2.5
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new Metadata();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingInfo(advertisingParams);

return adSettings;
}
```

* Uppräkningen `MetadataKeys` ersätter `DefaultMetadataKeys`. Alla nycklar i `DefaultMetadataKeys` finns inte i den nya versionen.

```java
//TVSDK v1.4
if (this.mediaPlayer != null && this.mediaPlayer.getCurrentItem() != null) { MetadataNode resourceMetadata =
(MetadataNode) this.mediaPlayer.getCurrentItem().getResource().getMetadata();
VideoAnalyticsMetadata vaMetadata = (VideoAnalyticsMetadata)
resourceMetadata.getNode(DefaultMetadataKeys.
VIDEO_ANALYTICS_METADATA_KEY.getValue());
}

//TVSDK v2.5
if (resourceMetadata.containsKey(VideoAnalyticsMetadata.
VIDEO_ANALYTICS_METADATA_KEY)) {
JSONObject vaMetadataObj =
new JSONObject(resourceMetadata.
getValue(VideoAnalyticsMetadata. VIDEO_ANALYTICS_METADATA_KEY));
vaMetadata = parseVideoAnalyticsMetadata(vaMetadataObj);
}

} catch (JSONException e) { e.printStackTrace();
}
```

* Advertising metadata representeras nu av klassen `AdvertisingMetadata`, en underklass till Metadata, och lagras nu i `MediaPlayerItemConfig` i stället för `MediaResource`.

```java
//TVSDK v1.4
MetadataNode mediaMetadata = new MetadataNode();

if (stream.live) { mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(),
getAdSettingsForLive());
} else {
mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(), getAdSettingsForVod());
}
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

if (stream.live) {
AuditudeSettings adSettings = getAdSettingsForLive(); adSettings.setLivePreroll(true); mediaItemConfig.setAdvertisingMetadata(adSettings);
} else {
// Set the advertising parameters for VOD. mediaItemConfig.setAdvertisingMetadata(getAuditudeSettingsForVod());
}

// Create advertising metadata node Metadata mediaMetadata = new Metadata();

// Asset Url
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, mediaMetadata);
try {
mediaPlayer.replaceCurrentResource(playerResource, mItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
//handle exception.
}
```

Metadata för nätverkskonfiguration, som tidigare var medlem av klassen `MediaResource`, representeras nu av klassen `NetworkConfiguration` och lagras nu i `MediaPlayerItemConfig` i stället för `MediaResource`.

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);
...

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

NetworkConfiguration mediaNetworkConfiguration = mediaItemConfig.getNetworkConfiguration();
```

**Ändringar i TimedMetadata-parsning**

Tolkningen av `TimedMetadata` har ändrats i 2.5 med avseende på datatyperna för tolkning av ID3-taggen.

```java
//TVSDK v1.4
public void onTimedMetadata(TimedMetadata timedMetadata) { TimedMetadata.Type type = timedMetadata.getType();
if (type.equals(TimedMetadata.Type.ID3)){ PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata(); Set<String> keys = metadata.keySet();
for (String key : keys) {
String value = metadata.getValue(key); PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"Key = " + key + " Value = " + value);
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { parseSCTE35Tag(timedMetadata);
}
}
}

//TVSDK v2.5
public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { PMPDemoApp.logger.i(LOG_TAG + " inside"," ontimedmetadata"); TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata();

TimedMetadata.Type type = timedMetadata.getType(); if (type.equals(TimedMetadata.Type.ID3)) {
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata();
if (metadata != null) { PMPDemoApp.logger.i(LOG_TAG +
"::expandID3Metadata", "isEmpty " + metadata.isEmpty());
Set<String> keys = metadata.keySet(); PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"No of keys=" + keys.size());
String s;
for (String key : keys) {
byte[] value = metadata.getByteArray(key); s = new String(value);
if (key.equalsIgnoreCase("APIC"))
s = "SUPPRESSING BINARY DATA FOR ATTACHED PICTURE.";
PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"Key=" + key + ", Length=" + value.length + ", Value=" + s.trim());
}
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { PMPDemoApp.logger.i(LOG_TAG +
" inside ontimedmetadata"," ext"); parseSCTE35Tag(timedMetadata);
}
}
}
```

**Andra ändringar**

Följande ytterligare ändringar är tillgängliga i version 2.5:

* Metoden `notifyClick()` har flyttats från `MediaPlayerView` till `MediaPlayer`.

* `AdPolicySelector` är ett gränssnitt, inte en klass. Implementera alla dess metoder.
* `AdPolicyInfo` innehåller nu en lista med  `AdBreakTimelineItem`, inte  `AdBreakPlacement`.

* API-namnet för den abstrakta klassen `ContentResolver` har ändrats.
* `PlacementOpportunityDetector` är inte längre tillgängligt. Utöka i stället den abstrakta klassen `OpportunityGenerator`. Referensimplementeringen innehåller ett exempel på detta.

* Parametrarna för konstruktorn `AdBreakPlacement` är desamma, men i en annan ordning. Ett exempel på implementering finns i Reference Player-implementeringen som medföljer produkten.

## Ändringar i DRM {#changes-in-drm}

De flesta ändringar i den här versionen finns i DRM-lagret. I följande tabell visas ytterligare ändringar mellan versionerna 1.4 och 2.5:

| DRMManager-metod | Lyckade återanrop i 1.4 | Fel vid återanrop i 1.4 | Lyssnare i 2.5 |
|--- |--- |--- |--- |
| obtainLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| obtainPreviewLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| autentisera | DRMAuthenticationCompleteCallback | DRMOperationErrorCallback | DRMAuthenticateListener |
| createMetadataFromBytes | NA | DRMOperationErrorCallback | DRMErrorListener |
| initialize | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| joinLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| leaveLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| resetDRM | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| returnLicense | DRMLicenseReturnCompleteCallback | DRMOperationErrorCallback | DRMReturnLicenseListener |
| setAuthenticationToken | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| storeLicenseBytes | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |

```java
//TVSDK 1.4
private final MediaPlayer.DRMEventListener _drmEventListener = new MediaPlayer.DRMEventListener() {

@Override
public void onDRMMetadata(final DRMMetadataInfo drmMetadataInfo) { PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata available
// event and the play event, so launch the metadata interface
// and give it the loaded metadata bytes, but only once
_drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo == null ||
!DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG + "#onDRMMetadata", "DRM auth is not needed."); return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold
// between the current player time and the DRM metadata start
// time. For the time being, we resolve it as soon as we receive
// the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG + "#onDRMMetadata", "DRMManager is null."); return;
}
SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity()); String authUser =
sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG + "#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(long majorCode,
long minorCode, Exception e) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + majorCode + " 0x" + Long.toHexString(minorCode));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};

//TVSDK 2.5
private final DRMMetadataInfoEventListener drmMetadataInfoEventListener = new DRMMetadataInfoEventListener() {
@Override
public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { final DRMMetadataInfo drmMetadataInfo =
drmMetadataInfoEvent.getDRMMetadataInfo();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata
// available event and the play event, so launch the
// metadata interface and give it the loaded metadata
// bytes, but only once
drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo ==
null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG +
"#onDRMMetadata",
"DRM auth is not needed.");
return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold between
// the current player time and the DRM metadata start time. For the
// time being, we resolve it as soon as we receive the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG +
"#onDRMMetadata", "DRMManager is null.");
return;
}

SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity());
String authUser = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(int major,
int minor,
String erroString, String serverErrorURL) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + major +
" 0x" +
Long.toHexString(minor));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};
```

Den statiska `DRMManager`-instansen som var tillgänglig i 1.4 efter att mediaplayer har skapats är nu tillgänglig efter att händelseavlyssnaren `onDRMMetadataInfo` har utlösts.

## Ändringar relaterade till adaptiv bithastighet (ABR) {#adaptive-bitrate-abr-related-changes}

**Ändringar i konstanter**

Många konstanter har ändrat typen från `String` till `int`. Till exempel: `MediaResourceType`, `ABRControlParameters` och `MediaPlayerStatusChangeEvent`.

```java
//TVSDK v1.4
ABRControlParameters
private void setAbrControlParams() { SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity());
if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED,
PMPDemoApp.DEFAULT_ABR_ENABLED)) {
int initialBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE, 0);
int minBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE, 0);
int maxBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE, PMPDemoApp.DEFAULT_MAX_BIT_RATE);
int mbrPolicyAsInt =
getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, 0); ABRControlParameters.ABRPolicy abrPolicy = policyFromInt(mbrPolicyAsInt); abrPolicy = abrPolicy != null ?
abrPolicy : ABRControlParameters.ABRPolicy.ABR_MODERATE;
_mediaPlayer.setABRControlParameters(new ABRControlParameters(initialBitRate,
minBitRate, maxBitRate, abrPolicy));
}
}

//TVSDK v2.5
ABRControlParameters
private void setAbrControlParams() { ABRControlParametersBuilder abrBuilder =
new ABRControlParametersBuilder();

if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED, PMPDemoApp.DEFAULT_ABR_ENABLED)) {

abrBuilder.setInitialBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE,
ABRControlParameters.DEFAULT_ABR_INITIAL_BITRATE)); abrBuilder.setMinBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxPlayoutRate(getDoublePreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_PLAYOUT_RATE,
ABRControlParameters.DEFAULT_MAX_PLAYOUT_RATE)); abrBuilder.setMinTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxTrickPlayBandwidthUsage(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BANDWIDTH,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE));

switch (getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, -1)) {
case 0: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_CONSERVATIVE); break;
case 1: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_MODERATE); break;
case 2: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_AGGRESSIVE); break;
default: abrBuilder.setPolicy(ABRControlParameters.DEFAULT_ABR_POLICY);
}
}
_mediaPlayer.setABRControlParameters(abrBuilder.toABRControlParameters());
}
```

**Ändringar i konstruktorn ABRControlParameters**

Vissa parametrar har lagts till, vissa har bytt namn och andra har flyttats. Följande är konstruktorsignaturen i v1.4 och den nya signaturen i 2.5:

```java
//TVSDK v1.4
public ABRControlParameters(ABRPolicy abrPolicy,
int nInitialBitRate, int nMinBitRate,
int nMaxBitRate)

//TVSDK v2.5
public ABRControlParameters(int nInitialBitRate,
int nMinBitRate, int nMaxBitRate,
ABRPolicy abrPolicy,
int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate,
int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate)
```

## Felhändelser och hantering av {#error-events-and-handling}

**Ändringar i felhanteringen**

Klassen `MediaError` har ersatts med klassen `Notification`. Den enda skillnaden mellan klasserna `MediaError` och `Notification` är att de senare inte innehåller något description-attribut. Felkoderna TVSDK 1.4 med värdena 101xxx, 102xxx,104xxx,106xxx,107xxx,109xxx finns inte i TVSDK 2.5. Information om uppspelningskoderna i TVSDK 2.5 finns i [Inbyggda värden för videouppspelning](assets/psdk_android_2.5.pdf).

Nedan följer exempel på felhantering i TVSDK 1.4 och 2.5:

```java
//TVSDK v1.4
@Override
public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");

switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR: PMPDemoApp.logger.e(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: " + notification + "."); getActivity().finish();
break;
default:
// do nothing
}
}

//TVSDK v2.5
private final StatusChangeEventListener statusChangeEventListener = new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent mediaPlayerStatusChangeEvent)
{
MediaPlayerStatus state = mediaPlayerStatusChangeEvent.getStatus(); PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");
switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR:
PMPDemoApp.logger.e(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: ");
printErrorMetadata(mediaPlayerStatusChangeEvent.getMetadata()); showToast("MediaPlayer status ERROR: Look at the logs for details"); getActivity().finish();
break;
default:
// do nothing
}
}
};
```

Alla fel som kan återställas behandlas som varningar och hanteras med `NotificationEventListener` i TVSDK 2.5. Varningarna visas som meddelanden med `onOperationFailed`-avlyssnaren i QOS-hanteraren i TVSDK 1.4 där meddelandet är en separat händelse, precis som i TVSDK 2.5. Varningen som hanteras i 1.4 och 2.5 är följande:

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener()
{
@Override
public void onBufferStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
}
@Override
public void onBufferComplete() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
}
@Override
public void onSeekStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
}
@Override
public void onSeekComplete(long adjustedTime) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
}
@Override
public void onLoadInfo(LoadInfo loadInfo) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize() + " bytes, media duration: " + loadInfo.getMediaDuration() + "ms, download duration: " + loadInfo.getDownloadDuration() + "ms");
}
@Override
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - ").append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append

//TVSDK v2.5
private final NotificationEventListener notificationEventListener = new NotificationEventListener() {
/**
* An example of dumping the information within a Notification. Here, we don't handle the event in
* any way except to print a log message.
* @param event The NotificationEvent
*/
@Override
public void onNotification(NotificationEvent event) { Notification notification = event.getNotification(); Notification.Type type = notification.getType(); StringBuilder sb = new StringBuilder(); sb.append("[").append(type).append("]");
sb.append(" Player operation failed (").append(notification.getCode()).append(")"); Metadata metadata = notification.getMetadata();
if (metadata != null)
{
for (String key : metadata.keySet())
{
sb.append(", ").append(key).append(" = ").append(metadata.getValue(key));
}
}
Notification inner = notification.getInnerNotification(); if (inner != null) {
sb.append(" :: Inner Notification [").append(inner.getType()).append("](").append(inner.getCode()).append(")");
Metadata innerMetadata = inner.getMetadata(); if (innerMetadata != null) {
for (String iKey : innerMetadata.keySet()) { sb.append(", ").append(iKey).append(" =
").append(innerMetadata.getValue(iKey));
}
}
}
switch(type)
{
case ERROR:
PMPDemoApp.logger.e(LOG_TAG, sb.toString()); break;
case WARNING:
PMPDemoApp.logger.w(LOG_TAG, sb.toString()); break;
default:
PMPDemoApp.logger.i(LOG_TAG, sb.toString()); break;
}
showToast(sb.toString()); PMPDemoApp.logger.d(LOG_TAG, sb.toString());
}
};
```

**Nya undantag**

Medan TVSDK v1.4 använde en kombination av null-värden returneras fel och en mängd undantag ( `MediaPlayerException`, `IllegalStateException` och `IllegalArgumentException`), TVSDK v2.5 `generatesMediaPlayerException` för alla fel.

>[!NOTE]
>
>Om du vill ha information om ett MediaPlayerException kan du använda `getErrorCode()`.

Ett exempel på ändringen är nedan:

```java
//TVSDK v1.4
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (IllegalArgumentException e) { PrimetimeReference.logger.w(LOG_TAG +
"#setBufferControlParams",
"Unable to apply buffering params: " + e.getMessage() + ".");
}
}

//TVSDK v2.5
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (MediaPlayerException e) { PrimetimeReference.logger.w(LOG_TAG + "#setBufferControlParams", "Unable to apply buffering params: " + e.getMessage() + ".");
}
}
```

## Ändringar i QOS-parametrar {#changes-to-qos-parameters}

Det finns mindre ändringar i objektegenskaperna för QOSProvider:

* `TimeToFirstFrame` är inte tillgängligt i TVSDK 2.5.
* TVSDK 2.5 QOSProvider har en ny egenskap som avgör den upplevda bandbredden under en direktuppspelningssession.

```java
//TVSDK v1.4
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitrate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); setQosItem("Time to first frame", (int) playbackInformation.getTimeToFirstFrame()); setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); setQosItem("Last seek time", (int) playbackInformation.getLastSeekTime());
}

//TVSDK v2.5
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitRate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart());
setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare());
setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());
```

* `QOSEventListener::onOperationFailed()` finns inte längre i TVSDK 2.5. Varningarna som tidigare visades i den här händelseavlyssnaren visas nu i `NotificationEventListener::onNotification()`-händelseavlyssnaren.

* `QOSProvider event listeners onBufferStart()`, `onBufferComplete()`, `onSeekStart()`, `onSeekComplete()` och `onLoadInfo()` är enskilda händelseavlyssnare som är bundna till en mediaPlayer-instans.

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener() {

@Override
public void onBufferStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
@Override
public void onBufferComplete() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
hideBufferingSpinner();
}
@Override
public void onSeekStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
@Override
public void onSeekComplete(long adjustedTime) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " +
adjustedTime + ".");
_controlBar.setPosition(adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayer.PlayerState.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
@Override
public void onLoadInfo(LoadInfo loadInfo) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " +
loadInfo.getUrl() + ", size: " + loadInfo.getSize() +
" bytes, media duration: " +
loadInfo.getMediaDuration() + "ms, download duration: " +
loadInfo.getDownloadDuration() + "ms");
 
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - "). append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append(key).append(": ").
append(metadata.getValue(key));
}
}
innerNotification = innerNotification.getInnerNotification();
}
String errMsg = sb.toString(); PMPDemoApp.logger.w(LOG_TAG +
"::MediaPlayer.QOSEventListener#onOperationFailed()", errMsg);
showToast(errMsg);
}
};

//TVSDK v2.5
mediaPlayer.addEventListener(MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE,
loadInfoEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_BEGIN,
bufferingBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_END,
bufferingEndEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_BEGIN,
seekBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_END,
seekEndEventListener);
// Buffering events.
BufferingBeginEventListener bufferingBeginEventListener = new BufferingBeginEventListener() {
@Override
public void onBufferingBegin(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
};

BufferingEndEventListener bufferingEndEventListener = new BufferingEndEventListener() {
@Override
public void onBufferingEnd(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()",
"Buffering complete."); hideBufferingSpinner();
}
};

BufferPreparedEventListener bufferPreparedEventListener = new BufferPreparedEventListener() {
@Override
public void onBufferPrepared() {
}
};
// seek events.
SeekBeginEventListener seekBeginEventListener = new SeekBeginEventListener() {

@Override
public void onSeekBegin(SeekEvent seekEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
};
SeekEndEventListener seekEndEventListener = new SeekEndEventListener() {
@Override
public void onSeekEnd(SeekEvent seekEvent) {
double adjustedTime = seekEvent.getActualPosition();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
_controlBar.setPosition((long) adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayerStatus.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
};
/**
* LoadInformationEventListener that intercepts PSDK load info events
*/
private final LoadInformationEventListener loadInfoEventListener = new LoadInformationEventListener() {

@Override
public void onLoadInformation(LoadInformationEvent event) { LoadInformation loadInfo = event.getLoadInfomation(); PMPDemoApp.logger.i(
LOG_TAG + "::LoadInformationEventListener#onLoadInfomation()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize()
+ " bytes, download duration: "
+ loadInfo.getDownloadDuration() + "ms");
}
};
```

## Användbara resurser {#helpful-resources}

* Läs den fullständiga hjälpdokumentationen på [Adobe Primetime Learn &amp; Support](https://helpx.adobe.com/support/primetime.html)-sidan.