---
description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen MediaPlayerItemConfig eller direktuppspelningsbaserad med klassen MediaPlayerItemConfig.
seo-description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen MediaPlayerItemConfig eller direktuppspelningsbaserad med klassen MediaPlayerItemConfig.
seo-title: Konfig-klassmetoder för taggar
title: Konfig-klassmetoder för taggar
uuid: 3317fc8b-c13c-4e7d-8334-aa8cdf40fa05
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661

---


# Konfig-klassmetoder för taggar{#config-class-methods-for-tags}

Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen MediaPlayerItemConfig eller direktuppspelningsbaserad med klassen MediaPlayerItemConfig.

TVSDK tillämpar den globala konfigurationen automatiskt på alla medieströmmar som inte anger någon strömsspecifik konfiguration.

Du kan hantera de anpassade taggarna genom att använda både `PSDKConfig` och `MediaPlayerItemConfig` visa dessa metoder:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>Prenumerera på specifika anpassade taggar</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function get subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> Hämtar den aktuella listan med prenumerationstaggar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function set subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2">Anger listan med prenumerationstaggar som kommer att visas för programmet. <p>Ditt program prenumererar automatiskt på alla taggar som överförs via <span class="codeph"> taggar</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>Anpassa de annonstaggar som används av standardannonsdetektorn </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function get adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> Hämtar den aktuella listan med annonstaggar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function set adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> Anger listan med annonstaggar som ska användas som standardgenerator för affärsmöjlighet. </td> 
  </tr> 
 </tbody> 
</table>

Kom ihåg följande:

* Metoderna set tillåter inte att parametern tags innehåller null-värden.

   Om TVSDK påträffas genereras ett `IllegalArgumentException`.
* Det anpassade taggnamnet måste innehålla prefixet #.

   Exempel: `#EXT-X-ASSET` är ett korrekt anpassat taggnamn, men `EXT-X-ASSET` är felaktigt.
* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.

