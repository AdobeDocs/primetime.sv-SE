---
description: TVSDK hämtar information från FreeWheel och andra annonsservrar som tillhandahåller VAST-svar. FreeWheel ger, inom VAST-svar, information från tjänsten Moat. Tjänsten Moat räknar med en noggrannhet som bättre visar om kreatörerna fångar upp eller försummar en viss målgrupps intressen.
title: Annonsmätningar från Moat
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Lägg till mått från Moat{#ad-measurements-from-moat}

TVSDK hämtar information från FreeWheel och andra annonsservrar som tillhandahåller VAST-svar. FreeWheel ger, inom VAST-svar, information från tjänsten Moat. Tjänsten Moat räknar med en noggrannhet som bättre visar om kreatörerna fångar upp eller försummar en viss målgrupps intressen.

Moat är en tjänst som mäter och visar bilder för många olika användningsområden, från webbläsare till program. Moat genererar marknadsföringsanalysdata i realtid på flera plattformar.

XML för VAST-svar har en egenskap och ett element som koden kan läsa, den yttre egenskapen `Ad id` och det yttersta `Extension`-elementet. Oavsett vilket kan koden använda TVSDK för att spara både `Ad id`-informationen och `Extension`-informationen och sedan ordna informationen i en trädstruktur. Med den här organisationen kan koden hämta data från vilken nivå som helst och skicka dem vidare dit som helst. Värdet för den yttersta egenskapen `Ad id` gör att koden kan koordinera information från den associerade kampanjen.

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

Freewheel kan också ange egenskapen `id` i `Ad`-elementet, vilket visas i exemplet nedan.

```xml
<Ad id="118566" sequence="1">
```

Se API-dokumentationen för klassen `NetworkAdInfo`.
