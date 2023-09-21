---
description: Du kan välja en anpassad startpunkt för när du ska ange en DVR-ström i stället för standardbeteendet att ange DVR-strömmen i början med klassen ConfigProvider.
title: Välja en anpassad startpunkt för DVR
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Välja en anpassad startpunkt för DVR {#choosing-a-custom-starting-point-for-dvr}

Du kan välja en anpassad startpunkt för när du ska ange en DVR-ström i stället för standardbeteendet att ange DVR-strömmen i början med klassen ConfigProvider.

Ställa in starttiden via [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) klass:

1. Aktivera [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Ange starttid i [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Kontrollera att den anpassade startpositionen är aktiverad.
