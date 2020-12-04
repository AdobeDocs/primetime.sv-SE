---
description: I det här avsnittet visas ett exempel på en konfiguration som illustrerar koncept och form för konfigurationen.
seo-description: I det här avsnittet visas ett exempel på en konfiguration som illustrerar koncept och form för konfigurationen.
seo-title: Exempel på RBOP-konfiguration
title: Exempel på RBOP-konfiguration
uuid: fa5ead93-36c5-4ad1-947b-c4f1f2632d9b
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Exempel på RBOP-konfiguration {#sample-rbop-configuration}

I det här avsnittet visas ett exempel på en konfiguration som illustrerar koncept och form för konfigurationen.

I följande exempel på JSON-konfiguration definieras en pixelutdataprincip som anger följande:

* Begränsa dekryptering av videon till upplösningar 1 080 eller lägre
* Ange särskilda begränsningar för upplösningar på 720 och 480:

   * För 720-upplösning: kräva HDCP för digitala utdata, kräver *CGMS-A-skydd (Copy Generation Management System) - analog*-skydd för analoga utdata.
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

* Specifikationerna för `pixelCount` är en nivå ned i JSON-strukturen i avsnittet `pixelConstraints`.

* Inom varje pixelräkningsspecifikation anges utdataskydd för både digitala och analoga utdata.
* I specifikationerna för digitala utdata anges HDCP-versioner, även om klienten för närvarande inte stöder HDCP-versionshantering. Mer information finns i Frågor och svar.

