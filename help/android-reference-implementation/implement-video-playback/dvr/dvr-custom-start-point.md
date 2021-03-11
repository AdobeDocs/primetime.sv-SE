---
description: Du kan välja en anpassad startpunkt för när du ska ange en DVR-ström i stället för standardbeteendet att ange DVR-strömmen i början med klassen ConfigProvider.
title: Välja en anpassad startpunkt för DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Välja en anpassad startpunkt för DVR {#choosing-a-custom-starting-point-for-dvr}

Du kan välja en anpassad startpunkt för när du ska ange en DVR-ström i stället för standardbeteendet att ange DVR-strömmen i början med klassen ConfigProvider.

Så här anger du starttiden med klassen [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html):

1. Aktivera [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Ange starttiden i [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Kontrollera att den anpassade startpositionen är aktiverad.
