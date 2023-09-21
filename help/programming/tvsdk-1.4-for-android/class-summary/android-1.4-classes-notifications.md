---
description: Dessa klasser beskriver meddelanden om fel, varningar och vissa aktiviteter som TVSDK utfärdar för loggnings- och felsökningsändamål.
title: Meddelandeklasser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Meddelandeklasser{#notification-classes}

Dessa klasser beskriver meddelanden om fel, varningar och vissa aktiviteter som TVSDK utfärdar för loggnings- och felsökningsändamål.

Paket: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)  Paket: [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| Klassnamn | Beskrivning |
|---|---|
| MediaPlayerNotification. [Fel](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | En klass som beskriver meddelandet för ett fel som gör att spelaren avbryter uppspelningen. Det här är en [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) av meddelandetyp FEL. |
| MediaPlayerNotification. [Info](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | En klass som beskriver ett informationsmeddelande. Det här är en [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) av meddelandetypen INFO. |
| MediaPlayerNotification. [Varning](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | En klass som beskriver ett varningsmeddelande. Det här är en [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) av meddelandetypen VARNING. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | En klass som innehåller informationsmeddelanden, varningar och fel. Kapslar in objektrepresentationen av en enda meddelandehändelse i [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification. [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | Returnerar beskrivningen som är associerad med den angivna meddelandekoden. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | En klass som lagrar en logg med meddelandeobjekt. En cirkulär lista med [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) objekt som ger åtkomst till en historiklista för meddelandehändelser. Det innebär att det finns en lista med element, där varje element innehåller en separat förekomst av [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) klassen. (tum [session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) paket.) |
| NotificationHistory. [Objekt](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | En klass som definierar en post i den cirkulära listan i [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) och innehåller meddelandet och dess tidsstämpel. |
| MediaPlayerNotification. [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | En klass som innehåller de meddelandetyper som stöds. |
