---
title: Funktionschefer
description: Med funktionshanterare kan du styra enskilda funktioner utan att behöva gå igenom hela TVSDK för att söka efter en funktion som kan vara utspridd på flera platser.
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Funktionschefer {#feature-managers}

Med funktionshanterare kan du styra enskilda funktioner utan att behöva gå igenom hela TVSDK för att söka efter en funktion som kan vara utspridd på flera platser. Funktionshanterare komprimerar kod till en klass per funktion. Funktionshanteraren väntar på utlösare från TVSDK-händelser och informerar sedan klassen som använder funktionshanteraren för att hantera resultatet. Funktionshanteraren ger den information som krävs till klassen.

Funktionshanterarna utför följande uppgifter:

* **Utlöser TVSDK-funktioner.**
Detta är funktionsanrop som utlöser en TVSDK-funktion. Till exempel: `PlaybackManager.play()` anropas när spelarprogrammet behöver starta videouppspelningen.

* **Lyssnar på TVSDK-händelser.**
Funktionshanteraren måste lyssna på TVSDK-händelser för att få information från TVSDK. Till exempel: `AdsManager` lyssnar på TVSDK Ads-händelser som ska meddelas när annonsbrytningar börjar.

* **Skickar händelser till hanteraren.**
När funktionshanterarna har tagit emot och bearbetat händelser från TVSDK, kontaktar de klientsidan för att hantera händelsen. Till exempel efter `AdsManager` tar emot en starthändelse för annonsradbrytning, anger att spelarfragmentet ska återspegla den här ändringen i användargränssnittet (inaktivera navigeringsfältet, visa annonsövertäckningen osv.).

Primetimes referensimplementering innehåller följande funktionshanterare:

| Funktionshanteraren | Standardfil | Funktion |  |
|---|---|---|---|
| Videouppspelning | PlaybackManager | HLS-uppspelning och -kontroll, DVR-uppspelning och -kontroll, buffertkontroll och hantering av flera bithastigheter. | Obligatoriskt |
| Skydd av DRM-innehåll | DrmManager | Skydd av innehåll. | Obligatoriskt |
| Annonsinfogning | AdsManager | Annonsinfogning, inklusive Adobe Primetime annonsbeslut, direkt annonsbrytning och anpassad annonsbrytning. | Valfritt |
| Undertexter | CCManager | Undertexter och VTT. | Valfritt |
| Ljud med låg bindning | AAManager | Ljud med sen bindning. | Valfritt |
| QoS | QosManager | QoS-statistik | Valfritt |
| Tillstånd | EntitlementManager | Integrering av berättigande för autentisering i Primetime. | Valfritt |

Referensimplementeringen innehåller grundläggande standardklasser, som listas ovan, och motsvarande klasser med suffixet På. Standardklasserna innehåller TVSDK-standardbeteenden medan klasserna med On-suffixet innehåller all kod som krävs för att aktivera TVSDK-funktionen och lyssna på TVSDK-händelser för den funktionen.

* För valfria funktioner fungerar standardkoden som om funktionen är inaktiverad.
* Klasser med suffixet På fungerar som om funktionen är aktiverad.
