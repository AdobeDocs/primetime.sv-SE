---
description: Du kan globalt konfigurera anpassade taggnamn i TVSDK med klassen MediaPlayerItemConfig.
title: Konfig-klassmetoder för taggar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Konfig-klassmetoder för taggar {#config-class-methods-for-tags}

Du kan globalt konfigurera anpassade taggnamn i TVSDK med klassen MediaPlayerItemConfig.

TVSDK tillämpar automatiskt den globala konfigurationen på alla medieströmmar som inte anger någon strömspecifik konfiguration.

`MediaPlayerItemConfig` använder följande metoder för att hantera anpassade taggar:

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Prenumerera på specifika anpassade taggar</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags </span> </td> 
   <td colname="col2"> <p>Hämtar den aktuella listan med prenumerationstaggar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags(String[] taggar); </span> </td> 
   <td colname="col2"> <p>Anger listan med prenumerationstaggar som kommer att visas för programmet. </p> <p>Ditt program prenumererar automatiskt på alla taggar som överförs via <span class="codeph"> setAdTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Anpassa de annonstaggar som används av standardaffärsmöjlighetens identifierare</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags; </span> </td> 
   <td colname="col2"> <p>Hämtar den aktuella listan med annonstaggar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] taggar); </span> </td> 
   <td colname="col2"> <p>Anger listan med annonstaggar som ska användas som standardgenerator för affärsmöjlighet. </p> </td> 
  </tr> 
 </tbody> 
</table>

Kom ihåg följande:

* Metoderna set tillåter inte att parametern tags innehåller null-värden.

  Om TVSDK påträffas genereras ett `IllegalArgumentException`.
* Det anpassade taggnamnet måste innehålla `#` prefix.

  Till exempel: `#EXT-X-ASSET` är ett korrekt anpassat taggnamn, men `EXT-X-ASSET` är felaktigt.

* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.
