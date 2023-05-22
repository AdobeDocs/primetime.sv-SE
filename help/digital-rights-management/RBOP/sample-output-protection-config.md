---
description: I det här avsnittet visas ett exempel på en konfiguration som illustrerar koncept och form för konfigurationen.
title: Exempel på RBOP-konfiguration
exl-id: 0f40be83-9c7f-482b-ac42-9aa4e3f46f58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Exempel på RBOP-konfiguration {#sample-rbop-configuration}

I det här avsnittet visas ett exempel på en konfiguration som illustrerar koncept och form för konfigurationen.

I följande exempel på JSON-konfiguration definieras en pixelutdataprincip som anger följande:

* Begränsa dekryptering av videon till upplösningar 1 080 eller lägre
* Ange särskilda begränsningar för upplösningar på 720 och 480:

   * För 720-upplösning: kräva HDCP för digitala utdata, krav *Copy Generation Management System - analog* (CGMS-A) skydd för analoga utdata.
   * För 480-upplösning: kräva HDCP för digitala utdata, kräver inget skydd för analog

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
