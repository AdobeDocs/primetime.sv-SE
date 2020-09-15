---
description: När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den i form av ett TimedMetadata-objekt.
seo-description: När TVSDK identifierar en prenumerationstagg i spellistan/manifestet försöker spelaren automatiskt att bearbeta taggen och visa den i form av ett TimedMetadata-objekt.
seo-title: Timed metadata, klass
title: Timed metadata, klass
uuid: 3debfad4-084f-4fb5-b699-ea5e8fd1ed51
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# Timed metadata, klass{#timed-metadata-class}

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
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> Unik identifierare för tidsbestämda metadata. Det här värdet extraheras vanligtvis från attributet cue/tag ID. Annars anges ett unikt slumpmässigt värde. Använd <span class="codeph"> getId </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> metadata </span> </td> 
   <td colname="col02"> Metadata </td> 
   <td colname="col2"> Den bearbetade/extraherade informationen från den anpassade taggen för spelningslistan/manifestet. Använd <span class="codeph"> getMetadata </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> Sträng </td> 
   <td colname="col2"> Namnet på tidsbestämda metadata. Om typen är <span class="codeph"> TAG </span>representerar värdet cue/tag-namnet. Om typen är <span class="codeph"> ID3 </span>är den null. Använd <span class="codeph"> getName </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> tid </span> </td> 
   <td colname="col02"> long </td> 
   <td colname="col2"> Tidspositionen, i millisekunder, i förhållande till början av huvudinnehållet där dessa tidsbestämda metadata finns i strömmen. Använd <span class="codeph"> getTime </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> Typ </td> 
   <td colname="col2"> Typen för tidsbestämda metadata. Använd <span class="codeph"> getType </span>. 
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
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0, 
   >url="www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* Om extraheringen misslyckas på grund av ett anpassat taggformat, kommer metadataegenskapen att vara tom och programmet måste extrahera den faktiska informationen. Inget fel genereras i det här fallet.

| Element | Beskrivning |
|---|---|
| `public enum Type { TAG, ID3}` | Möjliga typer för tidsbestämda metadata. |
| `public TimedMetadata(Type type, long time, long id, String name, Metadata metadata);` | Standardkonstruktor (time är lokal direktuppspelningstid). |
| `public long getTime();` | Tidspositionen, i förhållande till början av huvudinnehållet, där dessa metadata infogades i strömmen. |
| `public Metadata getMetadata();` | De metadata som infogats i strömmen. |
| `public Type getType();` | Returnerar typen för tidsbestämda metadata. |
| `public long getId();` | Returnerar det ID som extraherats från attributen cue/tag. Annars anges ett unikt slumpmässigt värde. |
| `public String getName();` | Returnerar namnet på referenspunkten, som vanligtvis är HLS-taggnamnet. |

