---
description: Om du vill göra undertexter tillgängliga för din klientspelare måste du aktivera dem. Användaren kan aktivera eller inaktivera undertexter och välja formatering.
seo-description: Om du vill göra undertexter tillgängliga för din klientspelare måste du aktivera dem. Användaren kan aktivera eller inaktivera undertexter och välja formatering.
seo-title: Visa undertexter
title: Visa undertexter
uuid: 7057014a-b14a-4790-8f7f-37d7a1fb8194
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Visa undertexter {#expose-closed-captions}

Om du vill göra undertexter tillgängliga för din klientspelare måste du aktivera dem. Användaren kan aktivera eller inaktivera undertexter och välja formatering.

Visa undertexter:

1. Ange egenskapen `closedCaptionDisplayEnabled` i `PTMediaPlayer`-objektet.

   Om användaren har aktiverat undertexter visas texten i det här steget.

   >[!NOTE]
   >
   >Klientanvändaren aktiverar eller inaktiverar undertextning med hjälpmedelsinställningarna för iOS, och dessa inställningar innehåller även formateringsalternativ.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` egenskapen är inaktuell. Använd egenskapen `subtitlesOptions` för `PTMediaPlayerItem`. Se [Visa underrubriker](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) för att använda undertexter.