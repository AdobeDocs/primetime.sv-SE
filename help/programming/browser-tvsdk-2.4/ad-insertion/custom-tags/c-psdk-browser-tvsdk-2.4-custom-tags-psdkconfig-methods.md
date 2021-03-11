---
description: Du kan konfigurera egna taggnamn i en ström med klassen MediaPlayerItemConfig.
title: Konfig-klassmetoder för taggar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Konfig-klassmetoder för taggar{#config-class-methods-for-tags}

Du kan konfigurera egna taggnamn i en ström med klassen MediaPlayerItemConfig.

Så här skapar du en ny `MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

Här är lite information om hur `MediaPlayerItemConfig`-metoderna används för att hantera anpassade taggar:

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>Prenumerera på specifika anpassade taggar</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Hämtar den aktuella listan med prenumerationstaggar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>Anger en lista över prenumerationstaggar som visas för programmet. </p> <p>Ditt program prenumererar automatiskt på alla taggar som överförs via <span class="codeph"> adTags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>Anpassa de annonstaggar som används av standardannonsdetektorn  </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>Hämtar den aktuella listan med annonstaggar. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>Anger listan med annonstaggar som ska användas av standardgeneratorn för affärsmöjlighet. </p> </td> 
  </tr> 
 </tbody> 
</table>

Kom ihåg följande:

* Det anpassade taggnamnet måste innehålla prefixet `#`.

   Till exempel är `#EXT-X-ASSET` ett korrekt anpassat taggnamn, men `EXT-X-ASSET` är felaktigt.

* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.

