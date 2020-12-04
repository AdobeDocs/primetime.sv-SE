---
seo-title: Så här använder du implementeringen av Primetimes referens
title: Så här använder du implementeringen av Primetimes referens
uuid: 9eb262c4-d987-493a-92a4-311118c5f01e
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Så här använder du referensimplementeringen {#how-to-use-the-primetime-reference-implementation} för Primetime

Primetimes referensimplementering är en modulär spelare som har delats upp i enskilda funktioner som du enkelt kan ändra med specialiserade funktionshanterare. De här funktionshanterarna används som en brygga för att ansluta programmet och TVSDK-biblioteket.

Du kan använda referensimplementeringen på följande sätt:

* Använd det som det är utan att ändra någon kod (alla funktioner aktiveras med standardvärden).
* Använd det som referens för att förstå hur du använder TVSDK-biblioteket.
* Välj och välj vilka funktioner som gäller för programmet genom att stänga av de funktioner som du inte använder.
* Anpassa gränssnittskomponenterna utan att göra några ändringar i funktionerna.

Vi tillhandahåller referensimplementeringen Primetime för att hjälpa dig förstå TVSDK och enkelt ändra funktionshanterarna för att anpassa din spelare. Mer information om TVSDK-biblioteket finns i [TVSDK 1.4 for Android Programmer&#39;s Guide](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android.pdf).

Klicka [här](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/index.html) för att enkelt få åtkomst till API-dokumentationen för referensimplementering i Javadoc-format.
