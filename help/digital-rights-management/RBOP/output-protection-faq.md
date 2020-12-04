---
description: Vanliga frågor och svar om hur du använder upplösningsbaserat utdataskydd.
seo-description: Vanliga frågor och svar om hur du använder upplösningsbaserat utdataskydd.
seo-title: Vanliga frågor om RBOP
title: Vanliga frågor om RBOP
uuid: 7dcd337c-369a-474c-8768-409c48b5cee5
translation-type: tm+mt
source-git-commit: fa9e89dd63c8b4c9d6eee78258957cfd30c29088
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# RBOP FAQ {#rbop-faq}

Vanliga frågor och svar om hur du använder upplösningsbaserat utdataskydd.

* **F.** *När jag definierar ett krav på digitala utdata för en pixelbegränsning får jag tolknings-/formateringsfel när jag utelämnar HDCP-versionen, men jag har inga HDCP-krav. Hur ska jag konfigurera mitt krav på digitala utdata i det här fallet?* **S.** Eftersom HDCP-versionskontroll inte stöds i klienten rekommenderar Adobe att HDCP-versionen ställs in på  `1.0`. Detta säkerställer att konfigurationen är korrekt formaterad och semantiskt konsekvent i framtiden när HDCP-versionskontroll stöds. Följande kodutdrag visar en konfiguration med det här HDCP-värdet.

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

* **F.** *Är RBOP-pixelbegränsningarna diskreta eller intervallbaserade?* **A.** RBOP-pixelbegränsningar är intervallbaserade. Varje pixelantal definierar kraven för alla pixelantal som är mindre än eller lika med det angivna antalet eller upp till det största antalet som är mindre än det värdet om det finns mer än en pixelbegränsning. Med andra ord används värdena som högsta tröskelvärden för varje lodrätt pixelantal.

   Låt oss anta att en MBR-ström med lodräta upplösningar på 240, 480, 600, 720 och 1080 skickas till spelaren med följande RBOP-inställningar.

   **Inställningar för RBOP-princip:**

   * 720P - HDCP krävs
   * 480P - ingen OP

   Följande regler gäller för varje variant.

   **Strömmar:**

   * 240, 480: Båda är &lt;= 480; inget OP krävs och strömmarna läses in med eller utan HDCP.
   * 600, 720: Båda är &lt;= 720; HDCP krävs för uppspelning
   * 1080: > 720; strömmen är ett block som listas (fel returneras) eftersom den inte hittas i reglerna ovan.


* **F.** På vissa Android-enheter används inte de begränsningar för antal pixlar som jag har definierat exakt som de har definierats. Vad händer?

   **S.** Vissa Android-enheter rapporterar bildrutestorlekar som är något större än den normala storleken. Du kan åtgärda detta genom att justera bildrutestorleken ( `maxPixel` och `pixelCount`-inställningarna) uppåt med 20 pixlar. Du kan till exempel justera inställningarna för bildrutestorlek uppåt från:

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

   genomgående för alla instanser av `maxPixel` och `pixelCount`.

