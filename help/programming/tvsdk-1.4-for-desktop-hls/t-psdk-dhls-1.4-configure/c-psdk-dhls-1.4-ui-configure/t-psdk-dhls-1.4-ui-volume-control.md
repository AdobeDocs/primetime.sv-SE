---
description: Du kan ange en gränssnittskontroll för ljudvolymen.
title: Tillhandahåll volymkontroll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Tillhandahåll volymkontroll{#provide-volume-control}

Du kan ange en gränssnittskontroll för ljudvolymen.

1. Vänta tills MediaPlayer-instansen har en giltig status för det här kommandot.

   Alla lägen utom FRISLÄPPT är giltiga.
1. Anropa metoden för volyminställning på `MediaPlayer` -instans för att ange ljudvolymen.

   ```
   public function set volume(value:Number):void
   ```

   Värdet för volymen representerar den begärda volymen uttryckt som en del av den maximala volymen, där 0 är tyst och 1 är den maximala volymen.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Om den angivna volymen är </th> 
      <th colname="col2" class="entry"> Den resulterande volymen är </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> Mindre än 0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Mellan 0 och 1 </td> 
      <td colname="col2"> Den angivna volymen </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Större än 1 </td> 
      <td colname="col2"> Värdet dividerat med 100 och inställt på ett av följande värden: 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">Resultatet om det är mellan 0 och 1 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 om resultatet är större än 1 </li> 
      </ul> <p>Tips: Den här logiken hanterar värden som tillhandahålls från klienter baserat på tidigare versioner av 
      <span class="codeph">fraser/primetime-sdk-name</span>, där volymvärdena låg mellan 0 och 100. </p> </td> 
   </tr> 
   </tbody> 
   </table>
