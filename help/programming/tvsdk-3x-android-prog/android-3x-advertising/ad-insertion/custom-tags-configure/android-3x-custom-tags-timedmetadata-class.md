---
description: När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta och visa taggen i form av ett TimedMetadata-objekt.
seo-description: När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta och visa taggen i form av ett TimedMetadata-objekt.
seo-title: Timed metadata, klass
title: Timed metadata, klass
uuid: c7b1c1d7-48b3-43c7-aa21-f800d894976d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Timed metadata, klass {#timed-metadata-class}

När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta och visa taggen i form av ett TimedMetadata-objekt.

Klassen innehåller följande element:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b> Egenskap </b></th> 
   <th colname="col02" class="entry"> <b> Typ </b></th> 
   <th colname="col2" class="entry"> <b> Beskrivning </b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>Unik identifierare för tidsbestämda metadata. </p> <p>Det här värdet extraheras vanligtvis från attributet cue/tag ID. Annars anges ett unikt slumpmässigt värde. Använd <span class="codeph"> getId </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadata </span> </td> 
   <td colname="col02"> Metadata </td> 
   <td colname="col2"> <p>Den bearbetade/extraherade informationen från den anpassade taggen för spelningslistan/manifestet. Använd <span class="codeph"> getMetadata </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> Sträng </td> 
   <td colname="col2"> <p>Namnet på tidsbestämda metadata. Om typen är <span class="codeph"> TAG </span>representerar värdet cue/tag-namnet. Om typen är <span class="codeph"> ID3 </span>är den null. Använd <span class="codeph"> getName </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> tid </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> <p>Tidspositionen, i millisekunder, i förhållande till början av huvudinnehållet där dessa tidsbestämda metadata finns i strömmen. Använd <span class="codeph"> getTime </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> Typ </td> 
   <td colname="col2"> <p>Typen för tidsbestämda metadata. Använd <span class="codeph"> getType </span>. 
     <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
      <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAGG - anger att tidsbestämda metadata skapades från en tagg i spellistan/manifestet. </li> 
      <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - anger att tidsbestämda metadata skapades från en ID3-tagg i medieströmmen. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Kom ihåg följande:

* TVSDK extraherar automatiskt attributlistan till nyckelvärdepar och lagrar attributen i metadataegenskapen.

   >[!TIP]
   >
   >Komplexa data i anpassade taggar i manifestet, till exempel strängar med specialtecken, måste anges inom citattecken. Exempel:   >
   >
   >
   ```>
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url= 
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```  >
   >



* Om extraheringen misslyckas på grund av ett anpassat taggformat, kommer metadataegenskapen att vara tom och programmet måste extrahera den faktiska informationen. I det här fallet genereras inget fel.

<table id="table_1BAE98BF23F641A3A5709EBE37B327F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Element </b></th> 
   <th colname="col2" class="entry"> <b>Beskrivning</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public enum Type {TAG, ID3} </span> </td> 
   <td colname="col2"> <p>Möjliga typer för tidsbestämda metadata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public TimedMetadata(Type, long time, long id, String name, Metadata metadata); </span> </td> 
   <td colname="col2"> <p>Standardkonstruktor (time är lokal direktuppspelningstid). </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getTime(); </span> </td> 
   <td colname="col2"> <p>Tidspositionen, i förhållande till början av huvudinnehållet, där dessa metadata infogades i strömmen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Metadata getMetadata(); </span> </td> 
   <td colname="col2"> <p>De metadata som infogats i strömmen. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Type getType(); </span> </td> 
   <td colname="col2"> <p>Returnerar typen för tidsbestämda metadata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getId(); </span> </td> 
   <td colname="col2"> <p>Returnerar det ID som extraherats från attributen cue/tag. Annars anges ett unikt slumpmässigt värde. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public String getName(); </span> </td> 
   <td colname="col2"> <p>Returnerar namnet på referenspunkten, som vanligtvis är HLS-taggnamnet. </p> </td> 
  </tr> 
 </tbody> 
</table>