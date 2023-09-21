---
description: Frågor och svar om hur man använder upplösningsbaserat utdataskydd.
title: Vanliga frågor om RBOP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Vanliga frågor om RBOP {#rbop-faq}

Frågor och svar om hur man använder upplösningsbaserat utdataskydd.

* **Fråga.** *När jag definierar ett krav på digitala utdata för en pixelbegränsning får jag parsnings-/formateringsfel när jag utelämnar HDCP-versionen, men jag har inga HDCP-krav. Hur ska jag konfigurera mitt krav på digitala utdata i det här fallet?* **S.** Eftersom HDCP-versionskontroll inte stöds i klienten rekommenderar Adobe att du anger HDCP-versionen till `1.0`. Detta säkerställer att konfigurationen är korrekt formaterad och semantiskt konsekvent i framtiden när HDCP-versionskontroll stöds. Följande kodutdrag visar en konfiguration med det här HDCP-värdet.

  ```
  { "pixelConstraints":  
    [  
      { "pixelCount": 720, "digital":  
        [  
          {  
            "output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}  
          }  
        ]  
      }  
    ]  
  }
  ```

* **Fråga.** *Är RBOP-pixelbegränsningarna diskreta eller intervallbaserade?* **S.** RBOP-pixelbegränsningar är intervallbaserade. Varje pixelantal definierar kraven för alla pixelantal som är mindre än eller lika med det angivna antalet eller upp till det största antalet som är mindre än det värdet om det finns mer än en pixelbegränsning. Med andra ord används värdena som högsta tröskelvärden för varje lodrätt pixelantal.

  Låt oss anta att en MBR-ström med lodräta upplösningar på 240, 480, 600, 720 och 1080 skickas till spelaren med följande RBOP-inställningar.

  **Inställningar för RBOP-princip:**

   * 720P - HDCP krävs
   * 480P - ingen OP

  Följande regler gäller för varje variant.

  **Strömmar:**

   * 240, 480: Båda är &lt;= 480; inget OP krävs och strömmarna läses in med eller utan HDCP.
   * 600, 720: Båda är &lt;= 720; HDCP krävs för uppspelning
   * 1080: > 720. Strömmen är blocklistad (fel returnerat) eftersom den inte hittas i reglerna ovan.

* **Fråga.** På vissa Android-enheter används inte de begränsningar för antal pixlar som jag har definierat exakt som de har definierats. Vad händer?

  **S.** Vissa Android-enheter rapporterar bildrutestorlekar som är något större än den normala storleken. Du kan åtgärda detta genom att justera bildrutestorleken ( `maxPixel` och `pixelCount` inställningar) uppåt 20 pixlar. Du kan till exempel justera inställningarna för bildrutestorlek uppåt från:

  ```
  { 
      "maxPixel": 800, 
      "pixelConstraints": [ 
          { "pixelCount": 532, 
            "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
            "analog": {"output": "REQUIRED"} 
          }, 
  ... 
  ```

  till:

  ```
  { 
      "maxPixel": 820, 
      "pixelConstraints": [ 
          { "pixelCount": 552, 
            "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
            "analog": {"output": "REQUIRED"} 
          }, 
  ... 
  ```

  genomgående, för alla förekomster av `maxPixel` och `pixelCount`.
