---
description: Du kan välja en anpassad startpunkt för när du ska ange en DVR-ström i stället för standardbeteendet att ange DVR-strömmen i början med klassen ConfigProvider.
title: Välja en anpassad startpunkt för DVR
exl-id: 9813bf60-a91d-4376-a5fe-02311b73e8a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
