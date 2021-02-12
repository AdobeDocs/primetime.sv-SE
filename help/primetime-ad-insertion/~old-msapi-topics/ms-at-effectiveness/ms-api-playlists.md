---
description: Manifestservern returnerar överordnad spellistor i M3U8-format, enligt den föreslagna standarden för HTTP-direktuppspelning. Den består av en uppsättning olika TS-strömmar (Variant Transport Streams), som var och en innehåller renderingar av samma innehåll för olika bithastigheter och format. Adobe Primetime-annonsinfogning lägger till direktivet EXT-X-MARKER, som ska tolkas av klientvideospelare.
seo-description: Manifestservern returnerar överordnad spellistor i M3U8-format, enligt den föreslagna standarden för HTTP-direktuppspelning. Den består av en uppsättning olika TS-strömmar (Variant Transport Streams), som var och en innehåller renderingar av samma innehåll för olika bithastigheter och format. Adobe Primetime-annonsinfogning lägger till direktivet EXT-X-MARKER, som ska tolkas av klientvideospelare.
seo-title: EXT-X-MARKER-direktivet
title: EXT-X-MARKER-direktivet
uuid: e349bf89-b196-47b4-a362-9913fa28b2c6
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# EXT-X-MARKER-direktivet {#ext-x-marker-directive}

Manifestservern returnerar överordnad spellistor i M3U8-format, enligt den föreslagna standarden för HTTP-direktuppspelning. Den består av en uppsättning olika TS-strömmar (Variant Transport Streams), som var och en innehåller renderingar av samma innehåll för olika bithastigheter och format. Adobe Primetime-annonsinfogning lägger till direktivet EXT-X-MARKER, som ska tolkas av klientvideospelare.

Mer information om taggen EXT-X-MARKER finns i [Adobe Primetime HTTP Live Streaming Profile](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>Den här funktionen är bara tillgänglig om URL:en för bootstrap-manifestservern inte innehåller parametern `pttrackingmode`.

>[!NOTE]
>
>Taggen EXT-X-MARKER läggs till i annonssegment och inte i innehållssegment.

Utkaststandarden på [HTTP Live Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) beskriver innehållet i och formatet för variantspellistor. EXT-X-MARKER-taggen instruerar klienten att anropa ett återanrop. Den innehåller följande komponenter:

* **IDUnique-** identifierare (sträng) för den här callback-händelsen i programströmmens kontext.

* **** TYPEType (sträng) för callback-händelsen: PodBegin, PodEnd, PrerollPodBegin, PrerollPodEnd eller AdBegin

* **** LÄNGD (i sekunder) från början av det segment som innehåller taggen som direktivet gäller för.

* **** OFFSETOvalfritt. Förskjutningen (i sekunder) i förhållande till början av segmentuppspelningen när återanropet måste anropas.

   * `PodBegin` och  `PrerollPodBegin` innehåller beacon-information i DATA-attributet och aktiveras i början av segmentet. Taggen `OFFSET` är därför inte tillgänglig här.

   * `AdBegin` innehåller beacon-information i DATA-attributet och de taggar som används i början av det segmentet. Taggen `OFFSET` är inte heller tillgänglig här.

   * `PodEnd` och  `PrerollPodEnd` innehåller beacon-information i DATA-attributet men utlöses i slutet av det aktuella segmentet eftersom dessa taggar förväntas utlösas i slutet av sista segmentet i den sista annonsen i rutan. I det här fallet är `OFFSET` inställt på `<duration of segment>` för att ange att beacon ska utlösas i slutet av det aktuella segmentet.

* **** DATABase64-kodad sträng omsluten av dubbla citattecken som innehåller de data som ska skickas till programmet när återanropet anropas. Den innehåller annonsspårningsinformation som överensstämmer med specifikationerna för VMAP1.0 och VAST3.0.

* **COUNTN** Antal annonser som kommer att sammanfogas i reklambrytningen.

   Endast tillämpligt om TYPE-komponenten är inställd på PodBegin eller PrerollPodBegin.

* **Den** totala längden (i sekunder) för den fyllda annonsbrytningen.

   Endast tillämpligt om TYPE-komponenten är inställd på PodBegin eller PrerollPodBegin.

När du skapar callback-funktionen tolkar du EXT-X-MARKER-komponenterna enligt följande:

* När taggen innehåller `OFFSET` utlöser du återanropet vid den angivna förskjutningen i förhållande till början av innehållsuppspelningen i det segmentet. Annars startar du återanropet så snart innehållet i segmentet börjar spelas upp.
* Använd `DURATION` för att spåra annonsinnehållets förlopp och för att begära URL:er för att spåra händelser.
* Skicka `ID`, `TYPE` och `DATA` till återanropet.

Använd värdena `PrerollPodBegin` och `PrerollPodEnd` för `TYPE` för att bestämma vilket TS-segment som ska spelas upp först i live/linjära strömmar.

>[!NOTE]
>
>Värdena `PrerollPodBegin` och `PrerollPodEnd` är bara tillgängliga när en förrollsannons infogas i en direktström.

Manifestservern innehåller EXT-X-MARKER-taggar i följande segment:

* Det första segmentet i annonsbrytningen, för att spåra början av en annonsruta.
* Det första segmentet i annonsen, för att spåra start/slutförande/förlopp för en enskild annons i en reklamruta.
* Det sista segmentet i annonsbrytningen för att spåra slutet av en annonspunkt.

Manifestservern skickar ett `VMAP1.0-conformant` XML-dokument för att spåra början och slutet av varje annonsbrytning. Det är en filtrerad version av det VMAP1.0-svar som returneras av annonsservern, och innehåller främst spårningshändelserna som visas här:

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<vmap:VMAP xmlns:vmap="https://www.iab.net/vmap-1.0" version="1.0"> 
    <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start"> 
        <vmap:TrackingEvents> 
            <vmap:Tracking event="breakStart"> 
                https://MyServer.com/breakstart.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="breakEnd"> 
                https://MyServer.com/breakend.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="error"> 
                https://MyServer.com/error.gif 
            </vmap:Tracking> 
        </vmap:TrackingEvents> 
    </vmap:AdBreak> 
</vmap:VMAP> 
</AdTrackingFragment> 
</AdTrackingFragments>
```

För varje annonsskapare som manifestservern infogar i programinnehållet skickas ett VAST3.0-anpassat XML-dokument för att spåra annonsen. Varje XML-dokument innehåller ett `<InLine>`-element som beskriver den infogade linjära annonsen, eller ett `<Wrapper>`-element för radbrytningsannonser (d.v.s. länkade eller omdirigerade annonser) och eventuella tillhörande annonser och tillägg. Om VAST-svaret innehåller ett sekvensattribut, t.ex. när annonsen är en del av en ad pod, innehåller dokumentet det attributet. Nedan följer ett exempel på ett VAST3.0-kompatibelt XML-dokument för att spåra en enskild annons:

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<VAST xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"  
      version="3.0"  
      xsi:noNamespaceSchemaLocation="https://service.videoplaza.com/schema/iab/vast-3.0.xsd"> 
<Ad id="903395"> 
    <InLine> 
      <AdSystem version="1.0">Auditude</AdSystem> 
      <AdTitle/> 
      <Error>https://ad.qa.auditude.com/adserver/?ErrAd1=[ERRORCODE]</Error> 
      <Impression id="urn:aeid:903395">https://ad.qa.auditude.com/adserver/e?type=adimp&amp; 
                 cid=127860991&amp; 
                 z=50183&amp; 
                 a=903395&amp; 
                 s=ef8c51dc&amp; 
                 t=1355309735&amp; 
                 w=100000&amp; 
                 uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                 l=1355280906&amp; 
                 u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                 br=1&amp; 
                 sq=1&amp; 
                 pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                 ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                               ?Cashcash=[CACHEBUSTING] 
                               ?Asset=[ASSETURI] 
      </Impression> 
      <Creatives> 
        <Creative> 
          <Linear> 
            <Duration>00:00:15</Duration> 
            <TrackingEvents> 
              ... 
              <Tracking event="firstQuartile"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=25&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking>                
              <Tracking event="midpoint"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=50&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="firstQuartile"> 
                https://www.Tweeeen.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                       ?Cashcash=[CACHEBUSTING] 
                                       ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="midpoint"> 
                https://www.Fiftyyyy.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                        ?Cashcash=[CACHEBUSTING] 
                                        ?Asset=[ASSETURI] 
              </Tracking> 
              ... 
            </TrackingEvents> 
            <VideoClicks> 
              <ClickTracking> 
                https://www.MP4-Vid-ClickTrack.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                                  ?Cashcash=[CACHEBUSTING] 
                                                  ?Asset=[ASSETURI] 
              </ClickTracking> 
              <ClickThrough> 
                https://www.cnn.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                   ?Cashcash=[CACHEBUSTING] 
                                   ?Asset=[ASSETURI] 
              </ClickThrough> 
              ... 
            </VideoClicks> 
            <AdParameters>campaign_id=7012</AdParameters> 
            <MediaFiles> 
              ...            
            </MediaFiles> 
          </Linear> 
        </Creative> 
        <Creative> 
          <CompanionAds> 
            <Companion id="103" width="300" height="250"> 
              <StaticResource creativeType="image/jpeg"> 
                https://ad.qa.auditude.com/adserver/c/z=50183; 
                  l=1355280906; 
                  u=956c3cd141086a1da44dcae8ea4ed14a; 
                  uid=_CxLm0b1SeKD8KXco__5TQ; 
                  cid=127860991; 
                  s=ef8c51dc; 
                  t=1355309735; 
                  br=1; 
                  sq=1; 
                  pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur 
                    %3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8; 
                  ax=0%2c0%2c1720%2c0; 
                  w=100000; 
                  a=903395; 
                  a1=103/c300x250.jpeg 
              </StaticResource> 
              <CompanionClickThrough> 
                https://ad.qa.auditude.com/adserver/l/a=903395%3Ba1=103 
                  %3Ba2=1%3Bz=50183%3Bl=1355280906%3Bu=956c3cd141086a1da44dcae8ea4ed14a 
                  %3Bcid=127860991%3Bs=ef8c51dc%3Buid=_CxLm0b1SeKD8KXco__5TQ 
                  %3Bt=1355309735%3Bbr=1%3Bsq=1%3Bpod=id%3a1%2cctype%3al%2cptype 
                  %3ap%2cdur%3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8 
                  %3Bax=0%2c0%2c1720%2c0 
              </CompanionClickThrough> 
              <AdParameters>campaign_id=7012</AdParameters> 
            </Companion> 
          </CompanionAds> 
        </Creative> 
        ... 
      </Creatives> 
      <Extensions> 
        <Extension type="Behavior"> 
          ... 
        </Extension> 
      </Extensions> 
    </InLine> 
  </Ad> 
  </VAST> 
</AdTrackingFragment> 
</AdTrackingFragments> 
```
