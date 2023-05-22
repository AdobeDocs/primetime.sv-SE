---
description: Om du vill göra undertexter tillgängliga för din klientspelare måste du aktivera dem. Användaren kan aktivera eller inaktivera undertexter och välja formatering.
title: Visa undertexter
exl-id: 6383a2b2-04e3-4fe1-a573-5e1f1ef486ed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Visa undertexter {#expose-closed-captions}

Om du vill göra undertexter tillgängliga för din klientspelare måste du aktivera dem. Användaren kan aktivera eller inaktivera undertexter och välja formatering.

Visa undertexter:

1. I `PTMediaPlayer` objekt, ange `closedCaptionDisplayEnabled` -egenskap.

   Om användaren har aktiverat undertexter visas texten i det här steget.

   >[!NOTE]
   >
   >Klientanvändaren aktiverar eller inaktiverar undertextning med hjälp av hjälpmedelsinställningarna för iOS, och dessa inställningar innehåller även formateringsalternativ.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` egenskapen är inaktuell. Använd `subtitlesOptions` egenskap för `PTMediaPlayerItem`. Se [Visa undertexter](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) om du vill använda undertexter.
