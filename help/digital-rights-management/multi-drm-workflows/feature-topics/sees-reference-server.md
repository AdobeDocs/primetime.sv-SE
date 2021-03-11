---
description: Ett sätt att samordna licensiering och policystyrning är att bygga in dessa funktioner i en tillståndsserver. Adobe tillhandahåller den SEES-referenstillståndsserver som du kan arbeta med för att skapa en egen server.
title: Referensserver - exempel ExpressPlay-tillståndsserver (SEES)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Referensserver: Exempel på ExpressPlay-tillståndsserver (SEES) {#reference-server-sample-expressplay-entitlement-server-sees}

Ett sätt att samordna licensiering och policystyrning är att bygga in dessa funktioner i en tillståndsserver. Adobe tillhandahåller den SEES-referenstillståndsserver som du kan arbeta med för att skapa en egen server.

Referensservern SEES demonstrerar ExpressPlay-berättigandetjänsten och visar två tjänster: grundläggande tidsbaserat berättigande och enhetsbindningsberättigande.

SEES är byggt på två ExpressPlay Fairplay-tjänster:

1. Tjänst för uttryckstokenbegäran
1. Tjänst för hämtning av Expresdisplay-post

URL-formatet för ExpressPlay-tokenbegäran har två former, en för produktion, en för testmiljön:

**Produktion**: <span></span>https://fp-gen.{prod_domain}/hms/fp/token

**Test**: <span></span>https://fp-gen.test.expressplay.com/hms/fp/token

URL-formatet för hämtning av ExpressPlay-post har två former, en för produktion, en för testmiljön:

**Produktion**: <span></span>https://api.{prod_domain}/cmiapi/getrecord/

**Test**: <span></span>https://api.test.expressplay.com/cmiapi/getrecord/
