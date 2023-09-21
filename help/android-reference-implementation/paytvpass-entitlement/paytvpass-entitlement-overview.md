---
description: Du kan använda Adobe Primetime-autentisering för att hantera användarberättiganden i din spelare.
title: Ökning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Ökning {#overview}

Du kan använda Adobe Primetime-autentisering för att hantera användarberättiganden i din spelare.

Funktionshanteraren som kapslar in berättigandeflödena för Primetime-autentisering är `EntitlementManager`. Den här klassen kapslar in berättigandelogiken och delegerar arbetet till en annan plats.

Den här referensimplementeringen för Android använder Primetime-autentiseringen AccessEnabler, biblioteksversion 1.7.3. En stor del av implementeringen liknar det befintliga demoprogrammet som finns i AccessEnabler-biblioteket.

Mer information om Primetime-autentisering finns i dokumentationen på [Introduktion till programmerarintegrering](https://tve.helpdocsonline.com/introduction-to-programmer-integration).
