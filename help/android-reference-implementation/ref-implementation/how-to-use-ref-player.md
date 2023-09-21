---
title: Så här använder du implementeringen av Primetimes referens
description: Så här använder du implementeringen av Primetimes referens
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Så här använder du implementeringen av Primetimes referens {#how-to-use-the-primetime-reference-implementation}

Primetimes referensimplementering är en modulär spelare som har delats upp i enskilda funktioner som du enkelt kan ändra med specialiserade funktionshanterare. De här funktionshanterarna används som en brygga för att ansluta programmet och TVSDK-biblioteket.

Du kan använda referensimplementeringen på följande sätt:

* Använd det som det är utan att ändra någon kod (alla funktioner aktiveras med standardvärden).
* Använd det som referens för att förstå hur du använder TVSDK-biblioteket.
* Välj och välj vilka funktioner som gäller för programmet genom att stänga av de funktioner som du inte använder.
* Anpassa gränssnittskomponenterna utan att göra några ändringar i funktionerna.

Vi tillhandahåller referensimplementeringen Primetime för att hjälpa dig förstå TVSDK och enkelt ändra funktionshanterarna för att anpassa din spelare. Se dock [TVSDK 1.4 for Android Programmer&#39;s Guide](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android.pdf) för detaljerad information om TVSDK-biblioteket.

Om du vill ha enkel åtkomst till API-dokumentationen för referensimplementering i Javadoc-format klickar du på [här](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/index.html).
