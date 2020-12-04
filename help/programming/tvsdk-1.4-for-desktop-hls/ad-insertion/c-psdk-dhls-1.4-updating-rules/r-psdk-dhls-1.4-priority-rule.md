---
description: Prioritetsregeln definierar prioritetsordningen för annonskreatörerna som väljs för uppspelning från ett VAST/VMAP-svar.
keywords: priority rule;creative selection rules
seo-description: Prioritetsregeln definierar prioritetsordningen för annonskreatörerna som väljs för uppspelning från ett VAST/VMAP-svar.
seo-title: Prioritetsregler
title: Prioritetsregler
uuid: 8716758f-686e-4927-8605-19c36091db65
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Prioritetsregler{#priority-rules}

Prioritetsregeln definierar prioritetsordningen för annonskreatörerna som väljs för uppspelning från ett VAST/VMAP-svar.

## En prioritetsregel har följande attribut och möjliga värden:

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> Nyckel</th> 
   <th class="entry"> Typ</th> 
   <th class="entry"> Värden</th> 
   <th class="entry"> Beskrivning</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> prioritet</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> En array med små mime-typer som definierar den prioritet i vilken källkreatörer måste väljas för uppspelning.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> artikel</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td><span class="codeph"> värd</span></td> 
   <td>För närvarande stöds bara <span class="codeph"> host</span>. Det här attributet måste finnas när <span class="codeph"> matchar</span> och <span class="codeph"> värden</span>-attribut har definierats.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matchar</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td><span class="codeph"> flera</span></td> 
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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td><span class="codeph"> prioritet</span></td> 
   <td>Värdet måste alltid vara <span class="codeph"> prioritet</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> <p>TVSDK kommer att använda attributet <span class="codeph"> matchar</span> för <span class="codeph">-objektet</span> för den kreativa källan och matcha mot värdena som definieras i den här arrayen</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> stream</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td></td> 
   <td> <p>Värdet kan vara <span class="codeph"> vod</span> eller <span class="codeph"> live</span></p> </td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "
<b>type</b>": "
<b>priority</b>",
                    "
<b>stream</b>": "vod",
                    "
<b>priority</b>": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    ...
                },
            ]
        }
    }
}
```

