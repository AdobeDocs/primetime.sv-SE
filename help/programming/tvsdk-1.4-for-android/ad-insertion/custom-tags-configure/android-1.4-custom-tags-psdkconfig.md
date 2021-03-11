---
description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen MediaPlayerItemConfig.
title: Konfig-klassmetoder för taggar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Konfig-klassmetoder för taggar{#config-class-methods-for-tags}

Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen MediaPlayerItemConfig.

TVSDK tillämpar den globala konfigurationen automatiskt på alla medieströmmar som inte anger någon strömsspecifik konfiguration.

`MediaPlayerItemConfig` använder följande metoder för att hantera anpassade taggar:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Prenumerera på specifika anpassade taggar</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags()  </span> </td> 
   <td colname="col2"> Hämtar den aktuella listan med prenumerationstaggar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(String[] taggar);  </span> </td> 
   <td colname="col2"> Anger listan med prenumerationstaggar som kommer att visas för programmet. <p>Ditt program prenumererar automatiskt på alla taggar som överförs via <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Anpassa de annonstaggar som används av standardannonsdetektorn</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags();  </span> </td> 
   <td colname="col2"> Hämtar den aktuella listan med annonstaggar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] taggar);  </span> </td> 
   <td colname="col2"> Anger listan med annonstaggar som ska användas som standardgenerator för affärsmöjlighet. </td> 
  </tr> 
 </tbody> 
</table>

Kom ihåg följande:

* Metoderna set tillåter inte att parametern tags innehåller null-värden.

   Om TVSDK påträffas genereras ett `IllegalArgumentException`.
* Det anpassade taggnamnet måste innehålla prefixet #.

   Till exempel är `#EXT-X-ASSET` ett korrekt anpassat taggnamn, men `EXT-X-ASSET` är felaktigt.
* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.

