---
title: BEES - översikt
description: BEES - översikt
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---


# BEES-översikt{#bees-overview}

Du kan implementera en BEES (Back-end Entitlement Service) för att tillhandahålla anpassade berättiganden för din DRM-åtgärd i Primetime Cloud.

Primetime Cloud DRM använder anonym licensleverans som standard. Det innebär att alla licensbegäranden som skickas till Primetime Cloud DRM returnerar en giltig licens utan att några ytterligare autentiserings-/auktoriseringskontroller utförs (såvida du inte har tillämpat en principbegränsning som kräver att Adobe Primetime-autentisering används).

Licensbegäran innehåller DRM-principen som användes under paketeringen/krypteringen av innehållet. DRM-principen används för att generera den DRM-licens som returneras till klienten. I standardscenariot måste du fatta alla DRM-principbeslut när innehållet paketeras. Kunder som vill ha bättre kontroll över dessa arbetsflöden har följande alternativ:

1. Integrera Primetime-autentisering för att lägga till extra behörighetskontroller före uppspelning.
1. Skapa en lokal tillståndstjänst som Primetime Cloud DRM frågar efter innan någon enhet kan spela upp innehåll som du har packat.

Din lokala tillståndstjänst måste ge ett svar till Primetime Cloud DRM som innehåller följande två datadelar:

* `isAllowed`
* `drmPolicyToUse`

Dessa avgör om en enhet får spela upp innehållet och vilken DRM-princip som ska användas för att generera DRM-licensen (om `isAllowed` är true).

Det här dokumentet innehåller det du behöver göra för att uppnå alternativ 2 ovan: Implementera din egen lokala externa tillståndstjänst och gör den tillgänglig för Primetime Cloud DRM för innehåll som du har paketerat.
