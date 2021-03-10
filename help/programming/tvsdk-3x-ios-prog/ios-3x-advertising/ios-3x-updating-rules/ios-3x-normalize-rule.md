---
description: Regeln normalize definierar en URL-omvandling som ska användas på en kreativ källwebbadress som hämtas från ett VAST/VMAP-svar.
keywords: normalisera regel;regler för kreativt urval
title: Normalisera regler
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Normalisera regler {#normalize-rules}

Regeln normalize definierar en URL-omvandling som ska användas på en kreativ källwebbadress som hämtas från ett VAST/VMAP-svar.

**Tabell 2: Regeln normalize har följande attribut och möjliga värden:**

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
   <td>Värdet måste alltid vara <span class="codeph"> normalize</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> artikel</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td><span class="codeph"> värd</span></td> 
   <td>För närvarande stöds bara <span class="codeph"> host</span>. Det här attributet måste finnas när <span class="codeph"> matchar</span> och <span class="codeph"> värden</span>-attribut har definierats.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matchar</span></td> 
   <td></td> 
   <td></td> 
   <td>Möjliga värden:
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> - equals</li> 
     <li><span class="codeph"> ne</span> - inte lika med</li> 
     <li><span class="codeph"> co</span> - contains</li> 
     <li><span class="codeph"> nc</span> - not contains</li> 
     <li><span class="codeph"> sw</span> - börjar med</li> 
     <li><span class="codeph"> Nytt</span>  - slutar med</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td>TVSDK använder attributet <span class="codeph"> match</span> för <span class="codeph">-objektet</span> för källans kreativa del och matchar mot värdena som definieras i den här arrayen.</td> 
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
