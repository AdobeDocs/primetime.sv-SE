---
seo-title: Översikt
title: Översikt
uuid: f45c6b58-53c5-41e0-be3d-590231dd214a
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# AIR Publisher ID-verktyg {#air-publisher-id-utility}

När du skapar en AIR-fil genererar AIR Developer Tool (ADT) automatiskt ett utgivar-ID. Verktyget AIR Publisher ID ( [!DNL AdobePublisherIDUtility.jar]) beräknar utgivar-ID för ett AIR-program.

Utgivar-ID:t är unikt för certifikatet som du använder för att skapa en AIR-fil. Om du återanvänder samma certifikat för flera AIR-program har alla AIR-program samma utgivar-ID. En AIR-release som godkänns i version 1.5.2 lägger inte till det genererade utgivar-ID:t i en fil. Om du tänker använda en lista över tillåtna i ett AIR-program använder du det här verktyget för att fastställa utgivar-ID:t.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Utgivar-ID:t som används för att framtvinga listor i AIR är inte detsamma som det utgivar-ID som anges i programmets [!DNL application.xml] fil.

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

* 
   * `signaturefile`* anger en sökväg till AIR-programmets [!DNL signatures.xml] fil, som finns i [!DNL META-INF] programkatalogen

* `signingcert` anger det certifikat som används för att signera ett AIR-program

>[!NOTE]
>
>Om du vill fastställa utgivar-ID:t för ett Android-program måste du använda alternativet `-s` för att ange det certifikat som används för att signera Android-programpaketet (APK). Primetime DRM krävs för att skapa Android-program som kan spela upp DRM-skyddat innehåll i Primetime.