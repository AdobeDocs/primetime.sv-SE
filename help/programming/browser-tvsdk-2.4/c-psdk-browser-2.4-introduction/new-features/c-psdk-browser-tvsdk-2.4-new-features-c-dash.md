---
description: Webbläsare-TVSDK har stöd för ett antal DASH-funktioner som du kan implementera för att lägga till funktioner i dina videoprogram.
seo-description: Webbläsare-TVSDK har stöd för ett antal DASH-funktioner som du kan implementera för att lägga till funktioner i dina videoprogram.
seo-title: DASH-funktioner som stöds
title: DASH-funktioner som stöds
uuid: 299516a4-09ed-4b8a-b0bf-a04f204f385a
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# DASH-funktioner som stöds{#supported-dash-features}

Webbläsare-TVSDK har stöd för ett antal DASH-funktioner som du kan implementera för att lägga till funktioner i dina videoprogram.

* [Uppspelningsfunktioner för DASH Core](#dash-core-playback)
* [Avancerade uppspelningsfunktioner för DASH](#dash-advanced-playback)
* [Skyddsfunktioner för DASH-innehåll](#dash-content-protection)
* [Funktioner för annonsinfogning i DASH Core](#dash-core-ad-insertion)
* [Avancerade funktioner för annonsinfogning i DASH](#dash-advanced-insertion-features)
* [DASH-integreringar](#dash-integrations)

>[!TIP]
>
>I tabellen nedan i funktionsmatrisen  ![](assets/supported15.png)
>betyder att funktionen stöds i den aktuella versionen.

Följande funktioner stöds:

<!-- 

<table id="table_lrb_p2g_xx"> 
 <title>DASH integrations</title> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col6" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Category </th> 
    <th colname="col2" class="entry"> Content type </th> 
    <th colname="col3" class="entry"> Feature </th> 
    <th colname="col6" align="center" class="entry"> 
     <lines>
       HTML5 FF, IE, Chrome, Android Chrome
     </lines> </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_14D9248BD1D8410E83AD27DB4AB3B6ED" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_EFA853CB763446B3B37F2CF6BCC53EE1" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Billing </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_B3A4E5937CEC4052977C08767219BC2B" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Browserify </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_3330E81B86C84AD391AEBFDFE911A47F" /> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## DASH-integreringar {#dash-integrations}

| Kategori | Innehållstyp | Funktion | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Integreringar | VOD + Live | Integrering med Adobe Analytics VHL | ![](assets/supported15.png) |
| Integreringar | VOD + Live | Fakturering | ![](assets/supported15.png) |
| Integreringar | VOD + Live | Browserify | ![](assets/supported15.png) |

## DASH - avancerade funktioner för annonsinfogning (CSAI) {#dash-advanced-insertion-features}

| Kategori | Innehållstyp | Funktion | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD | Endast annons | Stöds inte |
| Ad Insertion | VOD | Målparametrar | Endast VOD |
| Ad Insertion | VOD | Egna parametrar | Endast VOD |
| Ad Insertion | VOD + Live | Anpassad annonspolicy | Stöds inte |
| Ad Insertion | VOD + Live | Lazy och laddning | Stöds inte |
| Ad Insertion | VOD | Annonser, banners och klickbara annonser | Stöds inte |
| Ad Insertion | VOD | VPAID 2.0 | Stöds inte |

## Funktioner för infogning av annonser i DASH-kärnan (CSAI) {#dash-core-ad-insertion}

| Kategori | Innehållstyp | Funktion | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD + Live | Före rullning | Endast VOD |
| Ad Insertion | VOD + Live | Mid-roll | Endast VOD |
| Ad Insertion | VOD + Live | Efterrullning | Endast VOD |
| Ad Insertion | FER VOD | Annonsupplösning och beteenden | Stöds inte |
| Ad Insertion | VOD + Live | Standardannonspolicy | Endast VOD |
| Ad Insertion | VOD + Live | VAST 2.0/3.0 | Endast VOD |
| Ad Insertion | VOD + Live | VMAP 1.0 | Endast VOD |
| Ad Insertion | VOD + Live | CRS v3.1 | Endast VOD |

## Skyddsfunktioner för DASH-innehåll {#dash-content-protection}

<table id="table_hrb_p2g_xx">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Kategori </th> 
   <th colname="col2" class="entry"> Innehållstyp </th> 
   <th colname="col3" class="entry"> Funktion </th> 
   <th colname="col6" class="entry"> HTML5 FF, IE, Chrome, Android Chrome</th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Skydd av innehåll </td> 
   <td colname="col2"> VOD + Live </td> 
   <td colname="col3"> AES-128 </td> 
   <td colname="col6"> Stöds inte </td>
  </tr> 
  <tr> 
   <td colname="col1"> Skydd av innehåll </td> 
   <td colname="col2"> VOD + Live </td> 
   <td colname="col3"> Sample-AES </td> 
   <td colname="col6"> Stöds inte </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Skydd av innehåll </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3"> DRM </td> 
   <td colname="col6"> 
    <ul id="ul_irb_p2g_xx"> 
     <li id="li_C4643F2978BC4C8ABDB3E6C72C75A468">Widewin 
      <ul id="ul_7047EA49AA3F40FE8F90E0ED6C028D83"> 
       <li id="li_B575735388D74D789D56BF373A470A6D">Krom </li> 
       <li id="li_855146E4AC3A48E69B65F0022E1C0156">Firefox 47+ </li> 
       <li id="li_BC06B0A6EAAC4FC991C713775A8BB4DA">Kromecast </li> 
      </ul> </li> 
     <li id="li_D48B51C2208F423CB85D08886C2E1C66">PlayReady i Internet Explorer i Windows 8.1 och Edge </li> 
     <li id="li_2786AC19387241A296E015EE6FD07F2D">Adobe Access för Windows Firefox (endast video) </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Avancerade DASH-uppspelningsfunktioner {#dash-advanced-playback}

| Kategori | Innehållstyp | Funktion | HTML5, FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Uppspelning | VOD | Uppspelning vid förskjutning | ![](assets/supported15.png) |
| Uppspelning | VOD | Uppspelning med endast ljud | ![](assets/supported15.png) |
| Uppspelning | VOD | Trick play | ![](assets/supported15.png) |
| Uppspelning | VOD | Smidig testkörning | ![](assets/supported15.png) |
| Uppspelning | VOD + Live | ID3-parsning | Stöds inte |
| Uppspelning | VOD | Stöd för flera perioder | Endast VOD |
| Uppspelning | VOD + Live | Tokeniserade strömmar | Stöds inte |
| Uppspelning | VOD + Live | Fakturering | ![](assets/supported15.png) |
| Uppspelning | VOD + Live | Browserify | ![](assets/supported15.png) |

## Uppspelningsfunktioner för DASH-kärna {#dash-core-playback}

| Kategori | Innehållstyp | Funktion | HTML5 FF, IE, Chrome, Android Chrome |
|---|---|---|---|
| Uppspelning | VOD + Live | Allmän uppspelning (Play, Pause, Seek) | ![](assets/supported15.png) |
| Uppspelning | FER VOD | Allmän uppspelning (Play, Pause, Seek) | Stöds inte |
| Uppspelning | VOD + Live | Adaptiv bithastighet | ![](assets/supported15.png) |
| Uppspelning | VOD + Live | 608/708 bildtexter | ![](assets/supported15.png) |
| Uppspelning | VOD + Live | WebVTT | Endast VOD |
| Uppspelning | VOD + Live | Redundans | Endast VOD |
| Uppspelning | VOD + Live | QoS- och Player-meddelanden | ![](assets/supported15.png) |
| Uppspelning | VOD + Live | Stöd för cookie-rubriker | ![](assets/supported15.png) |
| Uppspelning | VOD + Live | Ange parametrar för buffertkontroll | ![](assets/supported15.png) |
| Uppspelning | VOD + Live | Ange kontroller för adaptiv bithastighet | ![](assets/supported15.png) |
| Uppspelning | VOD + Live | Anpassade taggar (EventStream) | Endast VOD (intern) |
| Uppspelning | VOD + Live | Ljud med låg bindning | Endast VOD |
| Uppspelning | VOD + Live | 302 omdirigering | Endast VOD |