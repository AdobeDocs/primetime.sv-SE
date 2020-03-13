---
seo-title: Användning av kommandorad
title: Användning av kommandorad
uuid: 54b1e867-c6cc-4355-b8e6-a7ec910bd33d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

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

* 
   * `signaturefile`* anger sökvägen till AIR-programmets signatures.xml-fil, som finns i [!DNL META-INF] programkatalogen

* `signingcert` anger det certifikat som används för att signera AIR-programmet

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Om du vill ta reda på utgivar-ID:t för ett iOS-program använder du alternativet och anger det certifikat som används för att signera iOS-programmet. `-s` ***Adobe Primetime krävs för att skapa iOS-program som kan spela upp åtkomstskyddat innehåll***.

