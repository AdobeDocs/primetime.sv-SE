---
description: Prioritetsregeln definierar prioritetsordningen för annonskreatörerna som väljs för uppspelning från ett VAST/VMAP-svar.
keywords: prioritetsregel;regler för kreativt urval
title: Prioritetsregler
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Prioritetsregler {#priority-rules}

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

