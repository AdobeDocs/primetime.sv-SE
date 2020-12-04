---
description: När Browser TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den som ett TimedMetadata-objekt.
seo-description: När Browser TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den som ett TimedMetadata-objekt.
seo-title: Timed metadata, klass
title: Timed metadata, klass
uuid: 3f276618-5f61-4b41-bd2d-78e7f32178d9
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Timed metadata-klass{#timed-metadata-class}

När Browser TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den som ett TimedMetadata-objekt.

Klassen `TimedMetadata` innehåller följande element:

<table id="table_5827A0626EDC45F68DC3E7644F3EFF69"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Egenskap </th> 
   <th colname="col02" class="entry"> Typ </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>type </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>Här är de tidsbestämda metadatatyperna: 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAGG - tidsbestämda metadata skapades från en tagg i spellistan/manifestet. </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 - tidsbestämda metadata skapades från en ID3-tagg i medieströmmen. </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>tid </p> </td> 
   <td colname="col02"> <p>Nummer </p> </td> 
   <td colname="col2"> <p>Den lokala tidspositionen (millisekunder) i förhållande till början av huvudinnehållet där dessa tidsbestämda metadata finns i strömmen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>Sträng </p> </td> 
   <td colname="col2"> <p>Den unika identifieraren för tidsbestämda metadata. </p> <p>Extraheras vanligtvis från attributet cue/tag ID om det finns. Annars är det ett unikt slumpvärde. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>Nummer </p> </td> 
   <td colname="col2"> <p>Namnet på tidsbestämda metadata. </p> <p>Om typen är TAG representerar värdet cue/tag-namnet. Om typen är ID3 är värdet null. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>innehåll </p> </td> 
   <td colname="col02"> <p>Sträng </p> </td> 
   <td colname="col2"> <p>Råinnehållet i tidsbestämda metadata. </p> <p>Om typen är TAG representerar värdet hela attributlistan för cue/tag. Om typ-ID3 anges är värdet null. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>metadata </p> </td> 
   <td colname="col02"> <p><span class="codeph"> Metadata</span> </p> </td> 
   <td colname="col2"> <p>Den bearbetade/extraherade informationen från den anpassade taggen för spelningslistan/manifestet. </p> </td> 
  </tr> 
 </tbody> 
</table>

