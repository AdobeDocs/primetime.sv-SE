---
title: Förhandsgranskning av licens
description: Förhandsgranskning av licens
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Förhandsgranskning av licens{#license-preview}

Klienten kan skicka en licensförhandsvisningsbegäran, vilket innebär att programmet kan utföra en förhandsgranskning innan användaren tillfrågas om att köpa innehållet för att avgöra om användarens dator uppfyller alla villkor som krävs för uppspelning.

*`License preview`* avser en kunds möjlighet att förhandsgranska licensen (för att se vilka rättigheter licensen tillåter) i stället för att förhandsgranska innehållet (visa en liten del av innehållet innan beslut om köp fattas). Vissa av de parametrar som är unika för varje dator är: tillgängliga utdata och skyddsstatus, tillgänglig körnings-/DRM-version och DRM-klientens säkerhetsnivå. I licensförhandsgranskningsläget kan körnings-/DRM-klienten testa licensserverns affärslogik och ge användaren information så att han eller hon kan fatta ett välgrundat beslut. Kunden kan alltså se hur en giltig licens ser ut, men skulle inte få nyckeln för att dekryptera innehållet. Stöd för licensförhandsgranskning är valfritt och endast nödvändigt om du implementerar en anpassad klient som använder den här funktionen.

Om du vill avgöra om kunden har skickat en begäran om förhandsgranskning eller om licenshämtning ringer du `LicenseRequestMessage.getRequestPhase()`och jämföra med `LicenseRequestMessage.RequestPhase.Acquire`
