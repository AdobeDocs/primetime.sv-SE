---
seo-title: Användning av kommandorad
title: Användning av kommandorad
uuid: 54b1e867-c6cc-4355-b8e6-a7ec910bd33d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# Kommandoradsanvändning {#command-line-usage}

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

* 
   * `signaturefile`* anger sökvägen till AIR-programmets signatures.xml-fil, som finns i  [!DNL META-INF] programkatalogen

* `signingcert` anger det certifikat som används för att signera AIR-programmet

>[!NOTE]
>
>Om du vill ta reda på utgivar-ID:t för ett iOS-program använder du alternativet `-s` och anger det certifikat som används för att signera iOS-programmet. ***Adobe Primetime krävs för att skapa iOS-program som kan spela upp åtkomstskyddat innehåll***.

