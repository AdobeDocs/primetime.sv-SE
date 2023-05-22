---
description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.
title: Konfig-klassmetoder för taggar
exl-id: b23bba25-ddab-4700-bae6-db1ee833eea2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Konfig-klassmetoder för taggar{#config-class-methods-for-tags}

Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.

TVSDK tillämpar den globala konfigurationen automatiskt på alla medieströmmar som inte anger någon strömsspecifik konfiguration.

`PTSDKConfig` använder följande metoder för att hantera anpassade taggar:

| **Prenumerera på specifika anpassade taggar** |
|---|
| `subscribedTags` | Hämtar den aktuella listan med prenumerationstaggar. |
| `setSubscribedTags` | Anger en lista över prenumerationstaggar som kommer att visas för programmet. |
| **Anpassa de annonstaggar som används av standardannonsdetektorn** |
| `adTags` | Hämtar den aktuella listan med annonstaggar. |
| `setAdTags` | Anger listan med annonstaggar som ska användas som standardgenerator för affärsmöjlighet. |

Kom ihåg följande:

* Metoderna set tillåter inte att parametern tags innehåller null-värden.
* Det anpassade taggnamnet måste innehålla prefixet #.

   #EXT-X-ASSET är till exempel ett korrekt anpassat taggnamn, men EXT-X-ASSET är felaktigt.
* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.
