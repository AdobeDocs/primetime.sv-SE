---
description: Om du vill göra undertexter tillgängliga för din klientspelare måste du aktivera dem. Användaren kan aktivera eller inaktivera undertexter och välja formatering.
title: Visa undertexter
exl-id: 57168c6e-a958-4a89-b22b-0c9f1cab3a49
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
   >`closedCaptionDisplayEnabled` egenskapen är inaktuell. Använd `subtitlesOptions` egenskap för `PTMediaPlayerItem`. Se [Visa undertexter](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) om du vill använda undertexter.
