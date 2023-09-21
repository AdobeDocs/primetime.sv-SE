---
title: Användning av kommandorad
description: Användning av kommandorad
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# Användning av kommandorad {#command-line-usage}

Använd följande syntax när du kör verktyget:

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `signaturefile` anger sökvägen till signatur.xml-filen för AIR-programmet, som finns i programmen [!DNL META-INF] katalog

* `signingcert` anger vilket certifikat som används för att signera AIR-programmet

>[!NOTE]
>
>Om du vill ta reda på utgivar-ID:t för ett iOS-program använder du `-s` och ange vilket certifikat som används för att signera iOS-programmet. ***Adobe Primetime krävs för att skapa iOS-program som kan spela upp åtkomstskyddat innehåll***.
