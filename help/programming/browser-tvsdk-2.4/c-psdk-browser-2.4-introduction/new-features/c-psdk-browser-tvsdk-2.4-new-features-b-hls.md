---
description: Webbläsare-TVSDK har stöd för ett antal HLS-funktioner som du kan implementera för att lägga till funktioner i dina videoprogram.
seo-description: Webbläsare-TVSDK har stöd för ett antal HLS-funktioner som du kan implementera för att lägga till funktioner i dina videoprogram.
seo-title: HLS-funktioner som stöds
title: HLS-funktioner som stöds
uuid: 033d81f8-cea4-4687-b2fb-1524d9164d39
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# HLS-funktioner som stöds {#supported-hls-features}

Webbläsare-TVSDK har stöd för ett antal HLS-funktioner som du kan implementera för att lägga till funktioner i dina videoprogram.

* [HLS Core-uppspelning](#hls-core-playback)
* [HLS Avancerade uppspelningsfunktioner](#hls-advanced-playback)
* [Funktioner för skydd av HLS-innehåll](#hls-content-protection)
* [HLS Core och infogningsfunktioner](#hls-core-ad-insertion)
* [HLS Avancerade funktioner för annonsinfogning](#hls-advanced-ad-insertion)
* [HLS-integrering](#hls-integrations)

>[!TIP]
>
>Ikonen ![som](assets/supported15.png) stöds i tabellen nedan betyder att funktionen stöds i den aktuella versionen.

>[!TIP]
>
>I Safari-kolumnen betyder &quot;Plattformsbegränsning&quot; att det inte finns stöd för användningsexemplet eftersom den plattformen inte tillåter implementering av stöd för det. Om du infogar något ska du använda SSAI. Om det finns uppspelningsbegränsningar som är viktiga för dig kan du tvinga fram en återgång till Flash på Safari tills plattformen har stöd för att infoga annonser.

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

Följande funktioner stöds:

<!-- 

Removed Nielsen row 
<table id="table_D9E2D82992554905A0A551CC71AFA189"> 
 <title>HLS integrations</title> 
 <tgroup cols="6"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col4" colwidth="*" /> 
  <colspec colnum="5" colname="col5" colwidth="*" /> 
  <colspec colnum="6" colname="col7" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" morerows="1" class="entry"> Category </th> 
    <th colname="col2" morerows="1" class="entry"> Content type </th> 
    <th colname="col3" morerows="1" class="entry"> Feature </th> 
    <th colname="col4" morerows="1" class="entry"> Flash </th> 
    <th namest="col5" nameend="col7" class="entry"> HTML5 </th> 
   </tr> 
   <tr> 
    <th colname="col5" class="entry"> FF, IE, Chrome, Android Chrome </th> 
    <th colname="col7" class="entry"> Safari, iOS Safari </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## HLS-integreringar {#hls-integrations}

| Kategori | Innehållstyp | Funktion | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Integreringar | VOD + Live | Integrering med Adobe Analytics VHL | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |

## HLS-funktioner för avancerad annonsinfogning (CSAI) {#hls-advanced-ad-insertion}

| Kategori | Innehållstyp | Funktion | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Annonsinfogning | VOD | Endast annons | Stöds inte | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Annonsinfogning | VOD + Live | Målparametrar | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Annonsinfogning | VOD + Live | Anpassad annonspolicy | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Annonsinfogning | VOD + Live | Lazy och laddning | ![ikon som stöds](assets/supported15.png) | Stöds inte | Plattformsbegränsning |
| Annonsinfogning | VOD | Annonser, banners och klickbara annonser | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Annonsinfogning | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## Funktioner för infogning av HLS-kärnannonser (CSAI) {#hls-core-ad-insertion}

| Kategori | Innehållstyp | Funktion | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Annonsinfogning | VOD + Live | Före rullning | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Annonsinfogning | VOD + Live | Mid-roll | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Annonsinfogning | VOD + Live | Efterrullning | Endast VOD | Endast VOD | Endast VOD |
| Annonsinfogning | FER VOD | Annonsupplösning och beteenden | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Annonsinfogning | VOD + Live | Standardannonspolicy | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Annonsinfogning | VOD + Live | VAST 2.0/3.0 | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Annonsinfogning | VOD + Live | VMAP 1.0 | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Annonsinfogning | VOD + Live | CRS v3.1 | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |

## Funktioner för skydd av HLS-innehåll {#hls-content-protection}

| Kategori | Innehållstyp | Funktion | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Skydd av innehåll | VOD + Live | AES-128 | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Skydd av innehåll | VOD + Live | Sample-AES | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Skydd av innehåll | VOD | DRM | Adobe Access | Stöds inte | FairPlay |

## Avancerade HLS-uppspelningsfunktioner {#hls-advanced-playback}

| Kategori | Innehållstyp | Funktion | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Uppspelning | VOD | Uppspelning vid förskjutning | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | VOD | Uppspelning endast av ljud | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | VOD | Trick play | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | VOD | Smidigt tricks | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Uppspelning | VOD + Live | ID3-parsning | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Stöds inte |
| Uppspelning | VOD + Live | Stöd för brytpunkter | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | VOD + Live | Tokeniserade strömmar | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Uppspelning | VOD + Live | Fakturering | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | VOD + Live | Browserify | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |

## HLS-kärnuppspelning {#hls-core-playback}

| Kategori | Innehållstyp | Funktion | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Uppspelning | VOD + Live | Allmän uppspelning (Play, Pause, Seek) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | FER VOD | Allmän uppspelning (Play, Pause, Seek) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | VOD + Live | Adaptiv bithastighet | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | VOD + Live | 608/708 bildtexter | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | VOD + Live | WebVTT | ![ikon som stöds](assets/supported15.png) | Endast VOD | Endast VOD |
| Uppspelning | VOD + Live | Manifestväxling vid fel | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) |
| Uppspelning | VOD + Live | Avancerad redundans | ![ikon som stöds](assets/supported15.png) | Endast VOD | Plattformsbegränsning |
| Uppspelning | VOD + Live | QoS och spelarmeddelanden | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Begränsat QoS-stöd |
| Uppspelning | VOD + Live | Stöd för cookie-rubriker | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Uppspelning | VOD + Live | Ange parametrar för buffertkontroll | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Uppspelning | VOD + Live | Ange kontroller för adaptiv bithastighet | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Uppspelning | VOD + Live | Egna taggar | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Uppspelning | VOD + Live | Ljud med låg bindning | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |
| Uppspelning | VOD + Live | 302 omdirigering | ![ikon som stöds](assets/supported15.png) | ![ikon som stöds](assets/supported15.png) | Plattformsbegränsning |