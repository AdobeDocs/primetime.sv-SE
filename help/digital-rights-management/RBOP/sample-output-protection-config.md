---
description: I det här avsnittet visas ett exempel på en konfiguration som illustrerar koncept och form för konfigurationen.
title: Exempel på RBOP-konfiguration
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Exempel på RBOP-konfiguration {#sample-rbop-configuration}

I det här avsnittet visas ett exempel på en konfiguration som illustrerar koncept och form för konfigurationen.

I följande exempel på JSON-konfiguration definieras en pixelutdataprincip som anger följande:

* Begränsa dekryptering av videon till upplösningar 1 080 eller lägre
* Ange särskilda begränsningar för upplösningar på 720 och 480:

   * För 720-upplösning: kräver HDCP för digitala utdata; kräver *Copy Generation Management System - analog* (CGMS-A) skydd för analoga utdata.
   * För 480-upplösning: kräver HDCP för digitala utdata; kräver inte skydd för analoga

```
{ 
  "pixelConstraints":  
    [ 
      { 
        "pixelCount": 720, 
        "digital": 
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "REQUIRED_CGMSA"} 
      }, 
      { 
        "pixelCount": 480, 
        "digital":  
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "NO_PROTECTION"} 
      } 
    ], 
  "maxPixel": 1080 
}
```

Observera följande om exempelkonfigurationen ovan:

* The `pixelCount` -specifikationerna är en nivå ned i JSON-strukturen, inom `pixelConstraints` -avsnitt.

* Inom varje pixelräkningsspecifikation anges utdataskydd för både digitala och analoga utdata.
* I specifikationerna för digitala utdata anges HDCP-versioner, även om klienten för närvarande inte stöder HDCP-versionshantering. Mer information finns i Frågor och svar.
