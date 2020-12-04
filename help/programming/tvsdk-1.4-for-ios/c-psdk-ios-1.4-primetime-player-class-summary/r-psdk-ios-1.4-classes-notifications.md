---
description: Dessa klasser beskriver meddelanden om fel, varningar och vissa aktiviteter som TVSDK utfärdar för loggnings- och felsökningsändamål.
seo-description: Dessa klasser beskriver meddelanden om fel, varningar och vissa aktiviteter som TVSDK utfärdar för loggnings- och felsökningsändamål.
seo-title: Meddelandeklasser
title: Meddelandeklasser
uuid: 08c29efe-245d-4a6d-80c6-cd561cbf3b5f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# Meddelandeklasser{#notification-classes}

Dessa klasser beskriver meddelanden om fel, varningar och vissa aktiviteter som TVSDK utfärdar för loggnings- och felsökningsändamål.

| Klassnamn | Beskrivning |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | En klass som beskriver meddelandet för ett fel som gör att spelaren avbryter uppspelningen. Detta är ett [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html)-meddelande av meddelandetypen FEL. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Visar alla meddelanden som skickas av Primetime Player-ramverket. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | En klass som innehåller informationsmeddelanden, varningar och fel. Kapslar in objektrepresentationen av en enda meddelandehändelse i [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | En klass som lagrar en logg med meddelandeobjekt [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html)-objekt som ger åtkomst till en historiklista för meddelandehändelser. Det innebär att det finns en lista med element, där varje element innehåller en separat instans av [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | En klass som definierar en post i den cirkulära listan i [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) och som innehåller meddelandet och dess tidsstämpel. |

