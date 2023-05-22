---
description: Du kan använda Adobe Primetime-autentisering för att hantera användarberättiganden i din spelare.
title: Översikt
exl-id: 0db18747-0ccb-4654-8f1d-9b51915b3652
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Översikt {#overview}

Du kan använda Adobe Primetime-autentisering för att hantera användarberättiganden i din spelare.

Funktionshanteraren som kapslar in berättigandeflödena för Primetime-autentisering är `EntitlementManager`. Den här klassen kapslar in berättigandelogiken och delegerar gränssnittsarbetet till en annan plats.

Den här referensimplementeringen för Android använder Primetime-autentiseringen AccessEnabler, biblioteksversion 1.7.3. En stor del av implementeringen liknar det befintliga demoprogrammet som finns i AccessEnabler-biblioteket.

Mer information om Primetime-autentisering finns i dokumentationen på [Introduktion till programmeringsintegrering](https://tve.helpdocsonline.com/introduction-to-programmer-integration).
