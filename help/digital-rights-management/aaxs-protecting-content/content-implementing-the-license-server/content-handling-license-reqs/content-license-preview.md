---
title: Förhandsgranska licens
description: Förhandsgranska licens
copied-description: true
exl-id: 283ee661-b1ee-46b9-9337-0497c97bd785
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Förhandsgranska licens{#license-preview}

Klienten kan skicka en licensförhandsvisningsbegäran, vilket innebär att programmet kan utföra en förhandsgranskning innan användaren tillfrågas om att köpa innehållet för att avgöra om användarens dator uppfyller alla villkor som krävs för uppspelning. *Förhandsgranska licens* avser klientens möjlighet att förhandsgranska licensen (för att se vilka rättigheter licensen tillåter) i stället för att förhandsgranska innehållet (visa en liten del av innehållet innan beslut om köp fattas). Några av de parametrar som är unika för varje dator är: tillgängliga utdata och skyddsstatus, tillgänglig körnings-/DRM-version och DRM-klientens säkerhetsnivå. I licensförhandsgranskningsläget kan körnings-/DRM-klienten testa licensserverns affärslogik och ge användaren information så att han eller hon kan fatta ett välgrundat beslut. Kunden kan alltså se hur en giltig licens ser ut, men skulle inte få nyckeln för att dekryptera innehållet. Stöd för licensförhandsgranskning är valfritt och endast nödvändigt om du implementerar en anpassad klient som använder den här funktionen.

Om du vill avgöra om kunden har skickat en begäran om förhandsgranskning eller om licenshämtning ringer du `LicenseRequestMessage.getRequestPhase()`och jämföra `LicenseRequestMessage.RequestPhase.Acquire`
