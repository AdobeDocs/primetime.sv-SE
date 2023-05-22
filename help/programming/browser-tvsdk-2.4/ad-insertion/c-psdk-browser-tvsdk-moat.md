---
title: Annonsmätning från Moat
description: Annonsmätning från Moat
copied-description: true
exl-id: 3d54ca34-0b75-4a8e-ab2d-bbe59683c2cf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Annonsmätning från Moat {#ad-measurement-from-moat}

TVSDK hämtar information från FreeWheel och andra adminstratörer som tillhandahåller VAST-svar. FreeWheel ger, inom VAST-svar, information från tjänsten Moat. Tjänsten Moat räknar med en noggrannhet som bättre visar att kreatörerna fångar upp eller försummar en viss målgrupps intressen.

Moat är en tjänst som mäter och visar bilder för många olika användningsområden, från webbläsare till program. Moat genererar marknadsföringsanalysdata i realtid på flera plattformar.

XML-koden för VAST-svar har en egenskap och ett element som koden kan läsa, den yttersta egenskapen för annons-id och det yttersta elementet för tillägg. Oavsett vilket kan koden använda TVSDK för att spara både annons-id-informationen och tilläggsinformationen och ordna informationen i en trädstruktur. Med den här organisationen kan koden hämta data från vilken nivå som helst och skicka dem vidare dit som helst. Värdet på den yttersta annons-id-egenskapen gör att koden kan koordinera information från den associerade kampanjen.

FreeWheel kan till exempel returnera data i ett Extensions-element. Nedan finns ett exempelelement.

```
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

Freewheel kan också ange egenskapen id i Ad-elementet, vilket visas i exemplet nedan.

```
<Ad id="118566" sequence="1">
```

Se API-dokumentationen för klassen AdobePSDK.NetworkAdInfo.
