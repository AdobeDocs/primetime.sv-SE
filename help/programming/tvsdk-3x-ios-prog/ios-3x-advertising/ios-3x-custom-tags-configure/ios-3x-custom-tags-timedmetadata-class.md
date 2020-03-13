---
description: När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den i form av ett PTTimedMetadata-objekt.
seo-description: När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den i form av ett PTTimedMetadata-objekt.
seo-title: Timed metadata, klass
title: Timed metadata, klass
uuid: d76b2a6b-2995-4559-b15d-82ded4c27eea
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Timed metadata, klass {#timed-metadata-class}

När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den i form av ett PTTimedMetadata-objekt.

Klassen innehåller följande element:

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Egenskap</b></th> 
   <th colname="col02" class="entry"><b>Typ</b> </th> 
   <th colname="col2" class="entry"><b>Beskrivning</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadataId</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span> </td> 
   <td colname="col2"> Unik identifierare för tidsbestämda metadata. Det här värdet extraheras vanligtvis från attributet cue/tag ID. Annars anges ett unikt slumpmässigt värde. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span></td> 
   <td colname="col2"> Namnet på tidsbestämda metadata. Om typen är <span class="codeph"> TAG</span>representerar värdet cue/tag-namnet. Om typen är <span class="codeph"> ID3</span>är den null. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> tid</span> </td> 
   <td colname="col02"><span class="codeph"> CMTime</span></td> 
   <td colname="col2"> Tidspositionen, i millisekunder, i förhållande till början av huvudinnehållet där dessa tidsbestämda metadata finns i strömmen. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> <span class="codeph"> PTTimedMetadataType</span></td> 
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
   >Komplexa data i anpassade taggar i manifestet, till exempel strängar med specialtecken, måste anges inom citattecken. Exempel:   >
   >
   >
   ```>
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```  >
   >



* Om extraheringen misslyckas på grund av ett anpassat taggformat innehåller egenskapen content alltid taggens rådata, som är strängen efter kolonet. Inget fel genereras i det här fallet.

| **Element** | **Beskrivning** |
|---|---|
| TAGG, ID3 | Möjliga typer för tidsbestämda metadata. |
| `@property (nonatomic, assign) CMTime time` | Tidspositionen, i förhållande till början av huvudinnehållet, där dessa metadata infogades i strömmen. |
| `@property (nonatomic, assign) PTTimedMetadataType type` | Returnerar typen för tidsbestämda metadata. |
| `@property (nonatomic, retain) NSString *metadataId` | Returnerar det ID som extraherats från attributen cue/tag. Annars anges ett unikt slumpmässigt värde. |
| `@property (nonatomic, retain) NSString *name` | Returnerar namnet på referenspunkten, som vanligtvis är HLS-taggnamnet. |