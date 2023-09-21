---
description: Regeln normalize definierar en URL-omvandling som ska användas på en kreativ källwebbadress som hämtas från ett VAST/VMAP-svar.
keywords: normalisera regel;regler för kreativt urval
title: Normalisera regler
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Normalisera regler {#normalize-rules}

Regeln normalize definierar en URL-omvandling som ska användas på en kreativ källwebbadress som hämtas från ett VAST/VMAP-svar.

**Tabell 2: Regeln normaliserar har följande attribut och möjliga värden:**

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"><b>Nyckel</b></th> 
   <th class="entry"><b>Typ</b></th> 
   <th class="entry"><b>Värden</b></th> 
   <th class="entry"><b>Beskrivning</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td><span class="codeph"> normalisera</span></td> 
   <td>Värdet måste alltid vara <span class="codeph"> normalisera</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> artikel</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td><span class="codeph"> värd</span></td> 
   <td>Endast för närvarande <span class="codeph"> värd</span> stöds. Attributet måste finnas när <span class="codeph"> matchar</span> och <span class="codeph"> values</span> -attribut definieras.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matchar</span></td> 
   <td></td> 
   <td></td> 
   <td>Möjliga värden:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - är lika med</li> 
     <li><span class="codeph"> ne</span> - inte lika med</li> 
     <li><span class="codeph"> co</span> - innehåller</li> 
     <li><span class="codeph"> nc</span> - innehåller inte</li> 
     <li><span class="codeph"> sw</span> - börjar med</li> 
     <li><span class="codeph"> new</span> - slutar med</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td>TVSDK använder <span class="codeph"> matchar</span> på <span class="codeph"> artikel</span> av källans kreativa innehåll och matcha mot värdena som definieras i den här arrayen.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> sök</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Ett reguljärt uttryck som ska användas på källans kreativa URL för att matcha.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ersätt</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> Ett reguljärt uttryck som ska användas på källans kreativa URL som ska ersättas baserat på matchningen.</td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                ...
                }
                {
                    "
<b>type</b>": "
<b>normalize</b>",
                    "
<b>item</b>": "host",
                    "
<b>matches</b>": "ew",
                    "
<b>values</b>": [
                        "redirector.gvt1.com"
                    ],
                    "
<b>find</b>": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "
<b>replace</b>": "videoplayback/$1/expire//$2/signature//"
                }                
            ]
        }
    }
}
```
