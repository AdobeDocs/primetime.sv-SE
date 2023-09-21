---
description: Om du vill göra undertexter tillgängliga för din klientspelare måste du aktivera dem. Användaren kan aktivera eller inaktivera undertexter och välja formatering.
title: Visa undertexter
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
