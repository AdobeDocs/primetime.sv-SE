---
seo-title: Funktionschefer
title: Funktionschefer
uuid: 3d78544e-4819-4122-bfd3-01522a067aa9
description: Med funktionshanterare kan du styra enskilda funktioner utan att behöva gå igenom hela TVSDK för att söka efter en funktion som kan vara utspridd på flera platser.
seo-description: Med funktionshanterare kan du styra enskilda funktioner utan att behöva gå igenom hela TVSDK för att söka efter en funktion som kan vara utspridd på flera platser.
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Funktionschefer {#feature-managers}

Med funktionshanterare kan du styra enskilda funktioner utan att behöva gå igenom hela TVSDK för att söka efter en funktion som kan vara utspridd på flera platser. Funktionshanterare komprimerar kod till en klass per funktion. Funktionshanteraren väntar på utlösare från TVSDK-händelser och informerar sedan klassen som använder funktionshanteraren för att hantera resultatet. Funktionshanteraren ger den information som krävs till klassen.

Funktionshanterarna utför följande uppgifter:

* **Utlöser TVSDK-funktioner.**
Detta är funktionsanrop som utlöser en TVSDK-funktion. Anropas till exempel `PlaybackManager.play()` när spelarprogrammet behöver starta videouppspelningen.

* **Lyssnar på TVSDK-händelser.**
Funktionshanteraren måste lyssna på TVSDK-händelser för att få information från TVSDK. Avlyssnar till exempel `AdsManager` TVSDK Ads-händelser som ska meddelas när annonsbrytningarna börjar.

* **Skickar händelser till hanteraren.**
När funktionshanterarna har tagit emot och bearbetat händelser från TVSDK, kontaktar de klientsidan för att hantera händelsen. Efter att `AdsManager` ha tagit emot en starthändelse för annonsradbrytning instruerar det spelarfragmentet att återspegla den här ändringen i användargränssnittet (inaktivera navigeringsfältet, visa annonsövertäckningen osv.).

Primetimes referensimplementering innehåller följande funktionshanterare:

| Funktionshanteraren | Standardfil | Funktion |  |
|---|---|---|---|
| Videouppspelning | PlaybackManager | HLS-uppspelning och -kontroll, DVR-uppspelning och -kontroll, buffertkontroll och hantering av flera bithastigheter. | Obligatoriskt |
| Skydd av DRM-innehåll | DrmManager | Skydd av innehåll. | Obligatoriskt |
| Annonsinfogning | AdsManager | Annonsinfogning, inklusive Adobe Primetime-annonsbeslut, direkt annonsbrytning och anpassad annonsbrytning. | Valfritt |
| Undertexter | CCManager | Undertexter och VTT-undertexter. | Valfritt |
| Ljud med låg bindning | AAManager | Ljud med sen bindning. | Valfritt |
| QoS | QosManager | QoS-statistik. | Valfritt |
| Tillstånd | EntitlementManager | Integrering av berättigande för autentisering i Primetime. | Valfritt |

Referensimplementeringen innehåller grundläggande standardklasser, som listas ovan, och motsvarande klasser med suffixet På. Standardklasserna innehåller TVSDK-standardbeteenden medan klasserna med On-suffixet innehåller all kod som krävs för att aktivera TVSDK-funktionen och lyssna på TVSDK-händelser för den funktionen.

* För valfria funktioner fungerar standardkoden som om funktionen är inaktiverad.
* Klasser med suffixet På fungerar som om funktionen är aktiverad.