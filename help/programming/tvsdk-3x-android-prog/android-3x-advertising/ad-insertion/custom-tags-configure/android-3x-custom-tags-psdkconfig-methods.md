---
description: Du kan globalt konfigurera anpassade taggnamn i TVSDK med klassen MediaPlayerItemConfig.
seo-description: Du kan globalt konfigurera anpassade taggnamn i TVSDK med klassen MediaPlayerItemConfig.
seo-title: Konfig-klassmetoder för taggar
title: Konfig-klassmetoder för taggar
uuid: b75aebac-4b94-4c42-bed4-3c17ad989cd1
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Konfig-klassmetoder för taggar {#config-class-methods-for-tags}

Du kan globalt konfigurera anpassade taggnamn i TVSDK med klassen MediaPlayerItemConfig.

TVSDK tillämpar automatiskt den globala konfigurationen på alla medieströmmar som inte anger någon strömspecifik konfiguration.

`MediaPlayerItemConfig` använder följande metoder för att hantera anpassade taggar:

**Prenumerera på specifika anpassade taggar**

| <b>Metod</b> | <b>Beskrivning</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | Hämtar den aktuella listan med prenumerationstaggar. |
| `public final void setSubscribedTags(String[] tags);` | Anger listan med prenumerationstaggar som kommer att visas för programmet.  Ditt program prenumererar automatiskt på alla taggar som överförs via `setAdTags`. |

**Anpassa de annonstaggar som används av standardannonsdetektorn**

| <b>Metod</b> | <b>Beskrivning</b> |
|--- |--- |
| `public final String[] getAdTags;` | Hämtar den aktuella listan med annonstaggar. |
| `public final void setAdTags(String[] tags);` | Anger listan med annonstaggar som ska användas som standardgenerator för affärsmöjlighet. |

Kom ihåg följande:

* Metoderna set tillåter inte att parametern tags innehåller null-värden.

   Om TVSDK påträffas genereras ett `IllegalArgumentException`.
* Det anpassade taggnamnet måste innehålla `#` prefixet.

   Exempel: `#EXT-X-ASSET` är ett korrekt anpassat taggnamn, men `EXT-X-ASSET` är felaktigt.

* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.