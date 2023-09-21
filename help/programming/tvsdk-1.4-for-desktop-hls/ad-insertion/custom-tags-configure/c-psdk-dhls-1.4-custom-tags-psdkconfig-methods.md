---
description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen MediaPlayerItemConfig eller direktuppspelningsbaserad med klassen MediaPlayerItemConfig.
title: Konfig-klassmetoder för taggar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Konfig-klassmetoder för taggar{#config-class-methods-for-tags}

Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen MediaPlayerItemConfig eller direktuppspelningsbaserad med klassen MediaPlayerItemConfig.

TVSDK tillämpar den globala konfigurationen automatiskt på alla medieströmmar som inte anger någon strömsspecifik konfiguration.

Båda `PSDKConfig` och `MediaPlayerItemConfig` visa följande metoder för att hantera anpassade taggar:

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
   <td colname="col2">Anger listan med prenumerationstaggar som kommer att visas för programmet. <p>Ditt program prenumererar automatiskt på alla taggar som överförs via <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>Anpassa de annonstaggar som används av standardaffärsmöjlighetens identifierare </b> </td> 
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

  Till exempel: `#EXT-X-ASSET` är ett korrekt anpassat taggnamn, men `EXT-X-ASSET` är felaktigt.
* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.
