---
description: Dessa klasser beskriver meddelanden om fel, varningar och vissa aktiviteter som TVSDK utfärdar för loggnings- och felsökningsändamål.
title: Meddelandeklasser
exl-id: 611a886b-a77a-4092-ab05-25e496fec8b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Meddelandeklasser{#notification-classes}

Dessa klasser beskriver meddelanden om fel, varningar och vissa aktiviteter som TVSDK utfärdar för loggnings- och felsökningsändamål.

| Klassnamn | Beskrivning |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | En klass som beskriver meddelandet för ett fel som gör att spelaren avbryter uppspelningen. Det här är en [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) av meddelandetyp FEL. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Visar alla meddelanden som skickas av Primetime Player-ramverket. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | En klass som innehåller informationsmeddelanden, varningar och fel. Kapslar in objektrepresentationen av en enda meddelandehändelse i [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | En klass som lagrar en logg med meddelandeobjekt [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) objekt som ger åtkomst till en historiklista för meddelandehändelser. Det innebär att det finns en lista med element, där varje element innehåller en separat förekomst av [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | En klass som definierar en post i den cirkulära listan i [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) och innehåller meddelandet och dess tidsstämpel. |
