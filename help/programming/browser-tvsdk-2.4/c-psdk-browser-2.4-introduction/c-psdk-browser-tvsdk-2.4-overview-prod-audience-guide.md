---
description: Den här handboken innehåller information om hur du utvecklar videospelarprogram med Browser TVSDK.
title: Produktöversikt och målgrupp
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Produktöversikt och målgrupp{#product-overview-and-audience}

Den här handboken innehåller information om hur du utvecklar videospelarprogram med Browser TVSDK.

## Produktöversikt {#section_1C66E736CEFD4246B7C7C99AADD48118}

Adobe Primetime Software Development Kit (Browser TVSDK) är en verktygslåda som gör att du kan lägga till avancerade videouppspelningsfunktioner, innehållsskydd och annonsering i webbläsarbaserade videospelarprogram. Webbläsarens TVSDK innehåller JavaScript-API:er för att bygga webbläsarbaserade videoprogram och inkluderar uppspelningsstöd i följande lägen:

* Endast HTML5
* HTML5 med autoblixt som reserv
* Flash alltid

Den här versionen innehåller API:erna för webbläsarens TVSDK och ett exempel på en referensimplementering.

### UI Framework

För att snabba upp gränssnittsutvecklingen för JavaScript-baserade videospelarprogram för webbläsare innehåller Browser TVSDK ett gränssnittsramverk som består av API:er för att:

* Inkludera standardkontroller för användargränssnitt som spela upp/pausa, volym och så vidare
* Lägg enkelt till (eller ta bort) avancerade gränssnittskontroller för uppspelning utan att ändra DOM-strukturen direkt
* Konfigurera enkelt beteendet för de associerade gränssnittskontrollerna
* Skapa anpassade gränssnittskontroller
* Användargränssnittet för spelaren skalas baserat på krav

Mer information om API:erna för gränssnittsramverket finns i [UI Framework for Browser TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html).

## Målgrupp {#section_DFC9DECC2E30426DBBDDEA4E288E666C}

I den här handboken förutsätts det att du förstår hur du utvecklar program och videospelare med JavaScript. Du kan implementera en videospelare och inkludera webbläsarens TVSDK-funktioner.