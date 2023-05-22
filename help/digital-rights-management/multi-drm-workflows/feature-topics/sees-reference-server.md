---
description: Ett sätt att samordna licensiering och policystyrning är att bygga in dessa funktioner i en tillståndsserver. Adobe tillhandahåller den SEES-referenstillståndsserver som du kan arbeta med för att skapa en egen server.
title: Referensserver - exempel ExpressPlay-tillståndsserver (SEES)
exl-id: aa5b63f4-dffc-4808-8aa6-6b8f63df592c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

**Produktion**: ht<span></span>tps://fp-gen.{prod_domain}/hms/fp/token

**Testa**: ht<span></span>tps://fp-gen.test.expressplay.com/hms/fp/token

URL-formatet för hämtning av ExpressPlay-post har två former, en för produktion, en för testmiljön:

**Produktion**: ht<span></span>tps://api.{prod_domain}/cmiapi/getrecord/

**Testa**: ht<span></span>tps://api.test.expressplay.com/cmiapi/getrecord/
