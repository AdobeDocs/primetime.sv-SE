---
description: När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den i form av ett TimedMetadata-objekt.
title: Timed metadata, klass
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Timed metadata-klass{#timed-metadata-class}

När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den i form av ett TimedMetadata-objekt.

Klassen innehåller följande element:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Egenskap </th> 
   <th colname="col02" class="entry"> Typ </th> 
   <th colname="col2" class="entry"> Beskrivning </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> innehåll</span> </td> 
   <td colname="col02"> Sträng </td> 
   <td colname="col2"> Råinnehållet i tidsbestämda metadata. Om typen är TAG representerar värdet hela attributlistan för cue/tag. Om ID3-typen är null. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> id</span> </td> 
   <td colname="col02"> Sträng </td> 
   <td colname="col2"> Unik identifierare för tidsbestämda metadata. Det här värdet extraheras vanligtvis från attributet cue/tag ID. Annars anges ett unikt slumpmässigt värde. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> metadata</span> </td> 
   <td colname="col02"> Metadata </td> 
   <td colname="col2"> Den bearbetade/extraherade informationen från den anpassade taggen för spelningslistan/manifestet. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"> Sträng </td> 
   <td colname="col2">Namnet på tidsbestämda metadata. Om typen är <span class="codeph"> TAG</span> representerar värdet cue/tag-namnet. Om typen är <span class="codeph"> ID3</span> är den null. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> tid</span> </td> 
   <td colname="col02"> Nummer </td> 
   <td colname="col2"> Tidspositionen, i millisekunder, i förhållande till början av huvudinnehållet där dessa tidsbestämda metadata finns i strömmen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> Sträng </td> 
   <td colname="col2">Typen för tidsbestämda metadata. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAGG - anger att tidsbestämda metadata skapades från en tagg i spellistan/manifestet. </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 - anger att tidsbestämda metadata skapades från en ID3-tagg i medieströmmen. </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

Kom ihåg följande:

* TVSDK extraherar automatiskt attributlistan till nyckelvärdepar och lagrar attributen i metadataegenskapen.

   >[!TIP]
   >
   >Komplexa data i anpassade taggar i manifestet, till exempel strängar med specialtecken, måste anges inom citattecken. Exempel:
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* Om extraheringen misslyckas på grund av ett anpassat taggformat, kommer metadataegenskapen att vara tom och programmet måste extrahera den faktiska informationen. Inget fel genereras i det här fallet.

| Element | Beskrivning |
|---|---|
| `TAG, ID3 ID3, TAG` | Möjliga typer för tidsbestämda metadata. |
| `public function TimedMetadata(type:String, time:Number, id:String, name:String, content:String, metadata:Metadata)` | Standardkonstruktor (time är lokal direktuppspelningstid). |
| `content:String` | Det råa innehållet i källtaggen för dessa tidsbestämda metadata. |
| `time:Number` | Tidspositionen, i förhållande till början av huvudinnehållet, där dessa metadata infogades i strömmen. |
| `metadata:Metadata` | De metadata som infogats i strömmen. |
| `type:String` | Returnerar typen för tidsbestämda metadata. |
| `id:String` | Returnerar det ID som extraherats från attributen cue/tag. Annars anges ett unikt slumpmässigt värde. |
| `name:String` | Returnerar namnet på referenspunkten, som vanligtvis är HLS-taggnamnet. |

