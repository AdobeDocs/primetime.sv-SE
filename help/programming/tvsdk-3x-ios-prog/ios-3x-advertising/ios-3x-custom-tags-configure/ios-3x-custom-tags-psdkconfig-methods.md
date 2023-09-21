---
description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.
title: Konfig-klassmetoder för taggar
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Konfig-klassmetoder för taggar {#config-class-methods-for-tags}

Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.

TVSDK tillämpar den globala konfigurationen automatiskt på alla medieströmmar som inte anger någon strömsspecifik konfiguration.

`PTSDKConfig` använder följande metoder för att hantera anpassade taggar:

| **Prenumerera på specifika anpassade taggar** |  |
|---|---|
| `subscribedTags` | Hämtar den aktuella listan med prenumerationstaggar. |
| `setSubscribedTags` | Anger listan med prenumerationstaggar som kommer att visas för programmet. |
| **Anpassa de annonstaggar som används av standardaffärsmöjlighetens identifierare** |
| `adTags` | Hämtar den aktuella listan med annonstaggar. |
| `setAdTags` | Anger listan med annonstaggar som ska användas som standardgenerator för affärsmöjlighet. |


Kom ihåg följande:

* Metoderna set tillåter inte att parametern tags innehåller null-värden.
* Det anpassade taggnamnet måste innehålla prefixet #.

  #EXT-X-ASSET är till exempel ett korrekt anpassat taggnamn, men EXT-X-ASSET är felaktigt.
* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.
