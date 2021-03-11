---
description: QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.
title: Spåra på fragmentnivå med hjälp av inläsningsinformation
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Spåra på fragmentnivå med hjälp av inläsningsinformation{#track-at-the-fragment-level-using-load-information}

QoS (Quality of Service) ger en detaljerad bild av hur videomotorn fungerar. TVSDK tillhandahåller detaljerad statistik om uppspelning, buffring och enheter.

TVSDK tillhandahåller även information om följande hämtade resurser:

1. Spellistor/manifestfiler
1. Filfragment
1. Spåra information om filer

   Du kan läsa QoS-information (Quality of Service) om hämtade resurser, som fragment och spår, från klassen `LoadInfo`.

1. Implementera händelseavlyssnaren `onLoadInfo` för återanrop.
1. Registrera händelseavlyssnaren, som TVSDK anropar varje gång ett fragment har hämtats.
1. Läs intressanta data från parametern `LoadInfo` som skickas till återanropet.

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
    <thead> 
      <tr> 
      <th colname="col01" class="entry"> Egenskap </th> 
      <th colname="col1" class="entry"> Typ </th> 
      <th colname="col2" class="entry"> Beskrivning </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> <p>Hämtningens varaktighet i millisekunder. </p> <p>TVSDK skiljer inte mellan den tid det tog för klienten att ansluta till servern och den tid det tog att hämta det fullständiga fragmentet. Om till exempel ett 10 MB-segment tar 8 sekunder att ladda ned, tillhandahåller TVSDK den informationen, men talar inte om för dig att det tog 4 sekunder innan den första byten och ytterligare 4 sekunder att ladda ned hela fragmentet. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> Medielängden för de hämtade fragmenten i millisekunder. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> Tidslinjens periodindex som är associerat med den hämtade resursen. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> size  </span> </td> 
      <td colname="col1"> <span class="codeph"> long  </span> </td> 
      <td colname="col2"> Storleken på den hämtade resursen i byte. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <span class="codeph"> int  </span> </td> 
      <td colname="col2"> Index för motsvarande spår, om det är känt. annars 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <span class="codeph"> Sträng  </span> </td> 
      <td colname="col2"> Namnet på motsvarande spår, om det är känt. annars null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <span class="codeph"> Sträng  </span> </td> 
      <td colname="col2"> Typ av motsvarande spår, om den är känd. annars null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type  </span> </td> 
      <td colname="col1"> <span class="codeph"> Sträng  </span> </td> 
      <td colname="col2"> Vad TVSDK laddade ned. Något av följande: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST - En spellista/ett manifest </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAGMENT - Ett fragment </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK - Ett fragment som är associerat med ett visst spår </li> 
      </ul> Ibland är det inte möjligt att identifiera resurstypen. Om detta inträffar returneras FILE. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <span class="codeph"> Sträng  </span> </td> 
      <td colname="col2"> Den URL som pekar på den hämtade resursen. </td> 
      </tr> 
    </tbody> 
   </table>
