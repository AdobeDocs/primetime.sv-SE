---
description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.
seo-description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.
seo-title: Konfig-klassmetoder för taggar
title: Konfig-klassmetoder för taggar
uuid: 1d3651a0-3b70-4d3a-8ced-663a9dad7205
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Konfig-klassmetoder för taggar{#config-class-methods-for-tags}

Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.

TVSDK tillämpar den globala konfigurationen automatiskt på alla medieströmmar som inte anger någon strömsspecifik konfiguration.

`PTSDKConfig` använder följande metoder för att hantera anpassade taggar:

| **Prenumerera på specifika anpassade taggar** |
|---|
| `subscribedTags` | Hämtar den aktuella listan med prenumerationstaggar. |
| `setSubscribedTags` | Anger listan med prenumerationstaggar som kommer att visas för programmet. |
| **Anpassa de annonstaggar som används av standardannonsdetektorn** |
| `adTags` | Hämtar den aktuella listan med annonstaggar. |
| `setAdTags` | Anger listan med annonstaggar som ska användas som standardgenerator för affärsmöjlighet. |

Kom ihåg följande:

* Metoderna set tillåter inte att parametern tags innehåller null-värden.
* Det anpassade taggnamnet måste innehålla prefixet #.

   #EXT-X-ASSET är till exempel ett korrekt anpassat taggnamn, men EXT-X-ASSET är felaktigt.
* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.

