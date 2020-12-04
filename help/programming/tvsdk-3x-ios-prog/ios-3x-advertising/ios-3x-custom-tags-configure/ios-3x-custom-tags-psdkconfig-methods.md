---
description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.
seo-description: Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.
seo-title: Konfig-klassmetoder för taggar
title: Konfig-klassmetoder för taggar
uuid: 27f1df0a-bbd3-4d80-820e-b659f2f33069
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Konfigurationsklassmetoder för taggar {#config-class-methods-for-tags}

Du kan konfigurera anpassade taggnamn i TVSDK globalt med klassen PTSDKConfig.

TVSDK tillämpar den globala konfigurationen automatiskt på alla medieströmmar som inte anger någon strömsspecifik konfiguration.

`PTSDKConfig` använder följande metoder för att hantera anpassade taggar:

| **Prenumerera på specifika anpassade taggar** |  |
|---|---|
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