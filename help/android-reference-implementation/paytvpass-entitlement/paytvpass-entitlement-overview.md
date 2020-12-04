---
description: Du kan använda Adobe Primetime-autentisering för att hantera användarberättiganden i din spelare.
seo-description: Du kan använda Adobe Primetime-autentisering för att hantera användarberättiganden i din spelare.
seo-title: Översikt
title: Översikt
uuid: defd718d-849b-4e79-8e0f-114c43c5bcf7
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Översikt {#overview}

Du kan använda Adobe Primetime-autentisering för att hantera användarberättiganden i din spelare.

Funktionshanteraren som kapslar in berättigandeflödena för Primetime-autentisering är `EntitlementManager`. Den här klassen kapslar in berättigandelogiken och delegerar gränssnittsarbetet till en annan plats.

Den här referensimplementeringen för Android använder Primetime-autentiseringen AccessEnabler, biblioteksversion 1.7.3. En stor del av implementeringen liknar det befintliga demoprogrammet som finns i AccessEnabler-biblioteket.

Mer information om Primetime-autentisering finns i dokumentationen på [Introduktion till programmerarintegrering](https://tve.helpdocsonline.com/introduction-to-programmer-integration).
