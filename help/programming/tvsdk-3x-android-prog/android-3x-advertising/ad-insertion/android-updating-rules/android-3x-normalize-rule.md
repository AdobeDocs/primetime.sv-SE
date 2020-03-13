---
description: Regeln normalize definierar en URL-omvandling som ska användas på en kreativ källwebbadress som hämtas från ett VAST/VMAP-svar.
keywords: normalize rule;creative selection rules
seo-description: Regeln normalize definierar en URL-omvandling som ska användas på en kreativ källwebbadress som hämtas från ett VAST/VMAP-svar.
seo-title: Normalisera regler
title: Normalisera regler
uuid: 8511000e-3a8a-42f3-b4be-d069d09112b0
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc

---


# Normalisera regler {#normalize-rules}

Regeln normalize definierar en URL-omvandling som ska användas på en kreativ källwebbadress som hämtas från ett VAST/VMAP-svar.

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
   <td>Värdet måste alltid vara <span class="codeph"> normaliserat</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> artikel</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td><span class="codeph"> värd</span></td> 
   <td>För närvarande stöds bara <span class="codeph"> värden</span> . Det här attributet måste finnas när <span class="codeph"> matchningar</span> och <span class="codeph"> värdeattribut</span> definieras.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matchar</span></td> 
   <td></td> 
   <td></td> 
   <td>Möjliga värden:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - lika med</li> 
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
   <td>TVSDK använder attributet <span class="codeph"> match</span> på <span class="codeph"> objektet</span> i källfilen som är kreativt och matchar mot värdena som definieras i den här arrayen.</td> 
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
