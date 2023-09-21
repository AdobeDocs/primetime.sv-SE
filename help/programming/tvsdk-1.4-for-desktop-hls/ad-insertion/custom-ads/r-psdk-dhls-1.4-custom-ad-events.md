---
description: TVSDK-spelaren skickar händelser för att visa anpassad annonsinläsningsstatus eller för att ignorera en annons som tar för lång tid att läsa in eller som innehåller fel. Dessa händelser definieras i events.CustomAdEvents.
title: Anpassade annonshändelser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

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
   <td colname="col2"> <p>Den anpassade annonsspelaren meddelar TVSDK-spelaren om förloppet för den anpassade annonsen. &amp;nbsp; </p> <p>The <span class="codeph"> currentTime </span> och <span class="codeph"> totalTime </span> av annonsen skickas med den här händelsen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> Den anpassade annonsen har börjat spelas upp och visas för läsaren.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStoppad </td> 
   <td colname="col2"> Den anpassade annonsen har slutat spelas upp. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->
