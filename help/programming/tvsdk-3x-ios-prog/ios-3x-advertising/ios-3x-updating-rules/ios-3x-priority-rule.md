---
description: Prioritetsregeln definierar prioritetsordningen för annonskreatörerna som väljs för uppspelning från ett VAST/VMAP-svar.
keywords: prioritetsregel;regler för kreativt urval
title: Prioritetsregler
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
   <th class="entry"><b>Nyckel</b></th> 
   <th class="entry"><b>Typ</b></th> 
   <th class="entry"><b>Värden</b></th> 
   <th class="entry"><b>Beskrivning</b></th> 
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
   <td>Endast för närvarande <span class="codeph"> värd</span> stöds. Attributet måste finnas när <span class="codeph"> matchar</span> och <span class="codeph"> values</span> -attribut definieras.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matchar</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td><span class="codeph"> flera</span></td> 
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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> Sträng</span></td> 
   <td><span class="codeph"> prioritet</span></td> 
   <td>Värdet måste alltid vara <span class="codeph"> prioritet</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> Array</span></td> 
   <td></td> 
   <td> <p>TVSDK använder <span class="codeph"> matchar</span> på <span class="codeph"> artikel</span> av källans kreativa innehåll och matcha mot värdena som definieras i arrayen</p> </td> 
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
