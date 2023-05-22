---
description: Du kan globalt konfigurera anpassade taggnamn i TVSDK med klassen MediaPlayerItemConfig.
title: Konfig-klassmetoder för taggar
exl-id: 0a07ebdf-7336-4d4d-b7df-294afb3fd606
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Konfig-klassmetoder för taggar {#config-class-methods-for-tags}

Du kan globalt konfigurera anpassade taggnamn i TVSDK med klassen MediaPlayerItemConfig.

TVSDK tillämpar automatiskt den globala konfigurationen på alla medieströmmar som inte anger någon strömspecifik konfiguration.

`MediaPlayerItemConfig` använder följande metoder för att hantera anpassade taggar:

**Prenumerera på specifika anpassade taggar**

| <b>Metod</b> | <b>Beskrivning</b> |
|--- |--- |
| `public final String[] getSubscribedTags` | Hämtar den aktuella listan med prenumerationstaggar. |
| `public final void setSubscribedTags(String[] tags);` | Anger en lista över prenumerationstaggar som kommer att visas för programmet.  Ditt program prenumererar automatiskt på alla taggar som överförs via `setAdTags`. |

**Anpassa de annonstaggar som används av standardannonsdetektorn**

| <b>Metod</b> | <b>Beskrivning</b> |
|--- |--- |
| `public final String[] getAdTags;` | Hämtar den aktuella listan med annonstaggar. |
| `public final void setAdTags(String[] tags);` | Anger listan med annonstaggar som ska användas som standardgenerator för affärsmöjlighet. |

Kom ihåg följande:

* Metoderna set tillåter inte att parametern tags innehåller null-värden.

   Om TVSDK påträffas genereras ett `IllegalArgumentException`.
* Det anpassade taggnamnet måste innehålla `#` prefix.

   Till exempel: `#EXT-X-ASSET` är ett korrekt anpassat taggnamn, men `EXT-X-ASSET` är felaktigt.

* Du kan inte ändra konfigurationen efter att medieströmmen har lästs in.
