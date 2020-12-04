---
seo-title: Förhandsgranska licens
title: Förhandsgranska licens
uuid: 3171647d-1437-48ab-9659-3eb363993618
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Licensförhandsgranskning{#license-preview}

Klienten kan skicka en licensförhandsvisningsbegäran, vilket innebär att programmet kan utföra en förhandsgranskning innan användaren tillfrågas om att köpa innehållet för att avgöra om användarens dator uppfyller alla villkor som krävs för uppspelning. *Förhandsgranskning av licenser avser* kundens möjlighet att förhandsgranska licensen (för att se vilka rättigheter licensen tillåter) i stället för att förhandsgranska innehållet (visa en liten del av innehållet innan beslut om köp fattas). Några av de parametrar som är unika för varje dator är: tillgängliga utdata och skyddsstatus, tillgänglig körnings-/DRM-version och DRM-klientens säkerhetsnivå. I licensförhandsgranskningsläget kan körnings-/DRM-klienten testa licensserverns affärslogik och ge användaren information så att han eller hon kan fatta ett välgrundat beslut. Kunden kan alltså se hur en giltig licens ser ut, men skulle inte få nyckeln för att dekryptera innehållet. Stöd för licensförhandsgranskning är valfritt och endast nödvändigt om du implementerar en anpassad klient som använder den här funktionen.

Om du vill ta reda på om klienten har skickat en förhandsgranskningsbegäran eller en licensförfrågan ringer du `LicenseRequestMessage.getRequestPhase()`och jämför den med `LicenseRequestMessage.RequestPhase.Acquire`
