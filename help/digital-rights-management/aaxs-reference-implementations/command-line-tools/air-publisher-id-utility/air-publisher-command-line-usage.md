---
title: Användning av kommandorad
description: Användning av kommandorad
copied-description: true
exl-id: 67056085-beb5-4f54-8962-369bc32d7907
source-git-commit: 79cab347d0daa01549fbf8a9b37bf0a91c14648e
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
