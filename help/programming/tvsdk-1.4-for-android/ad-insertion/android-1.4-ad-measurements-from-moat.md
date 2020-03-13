---
description: TVSDK hämtar information från FreeWheel och andra annonsservrar som tillhandahåller VAST-svar. FreeWheel ger, inom VAST-svar, information från tjänsten Moat. Tjänsten Moat räknar med en noggrannhet som bättre visar om kreatörerna fångar upp eller försummar en viss målgrupps intressen.
seo-description: TVSDK hämtar information från FreeWheel och andra annonsservrar som tillhandahåller VAST-svar. FreeWheel ger, inom VAST-svar, information från tjänsten Moat. Tjänsten Moat räknar med en noggrannhet som bättre visar om kreatörerna fångar upp eller försummar en viss målgrupps intressen.
seo-title: Annonsmätningar från Moat
title: Annonsmätningar från Moat
uuid: 73ef3a14-7ad6-4e67-8ad3-eabbeb898a09
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Annonsmätningar från Moat{#ad-measurements-from-moat}

TVSDK hämtar information från FreeWheel och andra annonsservrar som tillhandahåller VAST-svar. FreeWheel ger, inom VAST-svar, information från tjänsten Moat. Tjänsten Moat räknar med en noggrannhet som bättre visar om kreatörerna fångar upp eller försummar en viss målgrupps intressen.

Moat är en tjänst som mäter och visar bilder för många olika användningsområden, från webbläsare till program. Moat genererar marknadsföringsanalysdata i realtid på flera plattformar.

XML för VAST-svar har en egenskap och ett element som koden kan läsa, den yttersta `Ad id` egenskapen och det yttersta `Extension` elementet. Oavsett vilket kan koden använda TVSDK för att spara både `Ad id` informationen och `Extension` informationen och sedan ordna informationen i en trädstruktur. Med den här organisationen kan koden hämta data från vilken nivå som helst och skicka dem vidare dit som helst. Värdet för den yttersta `Ad id` egenskapen gör att koden kan koordinera information från den associerade kampanjen.

FreeWheel kan till exempel returnera data i ett Extensions-element. Nedan finns ett exempelelement.

```xml
<?xml version="1.0"?> 
<Extensions> 
  <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
      <MeasurementInfo renditionID="6398737" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions> 
```

Freewheel kan också ange egenskapen `id` i `Ad` elementet, vilket visas i exemplet nedan.

```xml
<Ad id="118566" sequence="1">
```

Mer information om klassen finns i API-dokumentationen `NetworkAdInfo`.
