---
description: Du kan använda Adobe Primetime-autentisering för att hantera användarberättiganden i din spelare.
title: Översikt
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# Översikt {#overview}

Du kan använda Adobe Primetime-autentisering för att hantera användarberättiganden i din spelare.

Funktionshanteraren som kapslar in berättigandeflödena för Primetime-autentisering är `EntitlementManager`. Den här klassen kapslar in berättigandelogiken och delegerar gränssnittsarbetet till en annan plats.

Den här referensimplementeringen för Android använder Primetime-autentiseringen AccessEnabler, biblioteksversion 1.7.3. En stor del av implementeringen liknar det befintliga demoprogrammet som finns i AccessEnabler-biblioteket.

Mer information om Primetime-autentisering finns i dokumentationen på [Introduktion till programmerarintegrering](https://tve.helpdocsonline.com/introduction-to-programmer-integration).
