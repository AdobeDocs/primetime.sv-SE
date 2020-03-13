---
description: TVSDK-spelaren skickar händelser för att visa anpassad annonsinläsningsstatus eller för att ignorera en annons som tar för lång tid att läsa in eller som innehåller fel. Dessa händelser definieras i events.CustomAdEvents.
seo-description: TVSDK-spelaren skickar händelser för att visa anpassad annonsinläsningsstatus eller för att ignorera en annons som tar för lång tid att läsa in eller som innehåller fel. Dessa händelser definieras i events.CustomAdEvents.
seo-title: Anpassade annonshändelser
title: Anpassade annonshändelser
uuid: 78e2ccf4-5943-4c60-84be-623182d9a300
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Anpassade annonshändelser{#custom-ad-events}

TVSDK-spelaren skickar händelser för att visa anpassad annonsinläsningsstatus eller för att ignorera en annons som tar för lång tid att läsa in eller som innehåller fel. Dessa händelser definieras i events.CustomAdEvents.

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Händelse </th> 
   <th colname="col2" class="entry"> Definition </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru </span> </td> 
   <td colname="col2"> Antalet gånger som användaren klickade på en anpassad annons. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError </span> </td> 
   <td colname="col2"> Ett fel uppstod med den anpassade annonsen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded </span> </td> 
   <td colname="col2"> Den anpassade annonsen har lästs in.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading </span> </td> 
   <td colname="col2"> Den anpassade annonsen läses in. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused </span> </td> 
   <td colname="col2"> Den anpassade annonsen har pausats. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed </span> </td> 
   <td colname="col2"> Den anpassade annonsen fortsätter att spelas upp efter en paus. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlaying </span> </td> 
   <td colname="col2"> Den anpassade annonsen spelas upp. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress </span> </td> 
   <td colname="col2"> <p>Den anpassade annonsspelaren meddelar TVSDK-spelaren om förloppet för den anpassade annonsen. &amp;nbsp; </p> <p>Den <span class="codeph"> aktuellatiden </span> och den totala <span class="codeph"> tiden </span> för annonsen skickas med den här händelsen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> Den anpassade annonsen har börjat spelas upp och visas för läsaren.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStoppad </td> 
   <td colname="col2"> Den anpassade annonsen har spelats upp. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

