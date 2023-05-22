---
description: Dessa klasser beskriver meddelanden om fel, varningar och vissa aktiviteter som är aktuella vid loggning och felsökning.
title: Meddelandeklasser
exl-id: d8af783f-1e80-4e50-89b8-97643ff6670b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Meddelandeklasser {#notification-classes}

Dessa klasser beskriver meddelanden om fel, varningar och vissa aktiviteter som är aktuella vid loggning och felsökning.

Paket: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| Klassnamn | Beskrivning |
|---|---|
| [Meddelande](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | En klass som innehåller informationsmeddelanden, varningar och fel. Kapslar in objektrepresentationen av en enda meddelandehändelse i [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | Returnerar beskrivningen som är associerad med den angivna meddelandekoden och tillhandahåller numeriska konstanter för meddelandeobjekt. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | En klass som lagrar en logg med meddelandeobjekt. En cirkulär lista med [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) objekt som ger åtkomst till en historiklista för meddelandehändelser. Det innebär att det finns en lista med element, där varje element innehåller en separat förekomst av [Meddelande](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) klassen. |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | En klass som definierar en post i den cirkulära listan i [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) och innehåller meddelandet och dess tidsstämpel. |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | En klass som innehåller de meddelandetyper som stöds. |
