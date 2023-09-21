---
description: TVSDK hämtar information från FreeWheel och andra annonsservrar som tillhandahåller VAST-svar. FreeWheel ger, inom VAST-svar, information från tjänsten Moat. Tjänsten Moat räknar med en noggrannhet som bättre visar om kreatörerna fångar upp eller försummar en viss målgrupps intressen.
title: Annonsmätningar från Moat
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Annonsmätningar från Moat{#ad-measurements-from-moat}

TVSDK hämtar information från FreeWheel och andra annonsservrar som tillhandahåller VAST-svar. FreeWheel ger, inom VAST-svar, information från tjänsten Moat. Tjänsten Moat räknar med en noggrannhet som bättre visar om kreatörerna fångar upp eller försummar en viss målgrupps intressen.

Moat är en tjänst som mäter och visar bilder för många olika användningsområden, från webbläsare till program. Moat genererar marknadsföringsanalysdata i realtid på flera plattformar.

XML för VAST-svar har en egenskap och ett element som koden kan läsa, det yttersta `Ad id` egenskap och yttersta `Extension` -element. Oavsett vilket kan koden använda TVSDK för att spara båda `Ad id` information och `Extension` och sedan organisera informationen i en trädstruktur. Med den här organisationen kan koden hämta data från vilken nivå som helst och skicka dem vidare dit som helst. Värdet för det yttersta `Ad id` -egenskapen gör att koden kan koordinera information från den associerade kampanjen.

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

Frihjulet kan även ställa in `id` -egenskapen i `Ad` som i exemplet nedan.

```xml
<Ad id="118566" sequence="1">
```

API-information finns i API-dokumentationen för klassen [NetworkAdInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/)
