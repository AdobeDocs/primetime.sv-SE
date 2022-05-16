---
title: Översikt
description: Översikt
copied-description: true
exl-id: 07f2ef0b-c6aa-4574-a3ae-18685a090cf2
source-git-commit: a1fc67b708f3d5821532d3827639adbadf15f6b4
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# AIR Publisher ID-verktyg {#air-publisher-id-utility}

När du skapar en AIR-fil genererar AIR Developer Tool (ADT) automatiskt ett utgivar-ID. Verktyget AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) används för att beräkna utgivar-ID:t för ett AIR-program.

Utgivar-ID:t är unikt för det certifikat som du använder för att skapa en AIR-fil. Om du återanvänder samma certifikat för flera AIR-program har alla AIR-program samma utgivar-ID. En AIR-version som godkänns i version 1.5.2 lägger inte till det genererade utgivar-ID:t i en fil. Om du tänker använda ett AIR-program tillåtelselista kan du därför använda det här verktyget för att fastställa utgivar-ID:t.

>[!NOTE]
>
>Utgivar-ID:t som används för användning i AIR tillåtelselista är inte samma som utgivar-ID:t som anges i programmets [!DNL application.xml] -fil.

## Kommandoradsanvändning för verktyget AIR Publisher ID {#air-publisher-id-utility-command-line-usage}

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

* `signaturefile` anger en sökväg till AIR-programmets [!DNL signatures.xml] -fil, som finns i programmen [!DNL META-INF] katalog

* `signingcert` anger det certifikat som används för att signera ett AIR-program

>[!NOTE]
>
>Om du vill ta reda på utgivar-ID:t för ett Android-program måste du använda `-s` för att ange det certifikat som används för att signera Android-programpaketet (APK). Primetime DRM krävs för att skapa Android-program som kan spela upp DRM-skyddat innehåll i Primetime.
