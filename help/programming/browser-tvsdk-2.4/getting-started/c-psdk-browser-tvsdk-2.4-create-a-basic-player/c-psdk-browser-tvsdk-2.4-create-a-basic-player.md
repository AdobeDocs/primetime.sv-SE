---
description: Om du vill använda Browser TVSDK måste du skapa och konfigurera en grundspelare. Om du vill spela upp videoinnehåll kan du skapa en grundläggande spelare på två sätt med webbläsarens TVSDK eller med gränssnittets ramverk.
title: Grundläggande spelare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Översikt {#basic-player-overview}

Om du vill använda Browser TVSDK måste du skapa och konfigurera en grundspelare. Om du vill spela upp videoinnehåll kan du skapa en grundläggande spelare på två sätt: med webbläsarens TVSDK, eller med gränssnittsramverket.

## Använda webbläsarens TVSDK {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Använd de API:er som finns i webbläsarens TVSDK direkt för att koda videospelaren. SDK ger dig ramverk och verktyg samt en referensspelare att arbeta utifrån.

>[!TIP]
>
>Om du vill se det här fungera i en referensspelare ska du inte ange några attribut med `videoDiv`.

## Använda gränssnittsramverket {#section_AE02384CFEF64A448C108232AB62A9FF}

Den här modulen används för att skapa instanser av spelaren, där varje instans är bunden till ett DOM-element (document object model) som tillhandahålls av anroparen. Förutom att ha en instans av Browser TVSDK är varje spelarinstans värd för ett antal kontroller som utgör användargränssnittet för spelaren.

Genomförandet av varje kontroll består av två aspekter:

* En `HTMLElement`, som är den visuella representationen av komponenten på skärmen
* En `Behavior` som hanterar `HTMLElement` och tillhandahåller ett API för interaktioner

Information om dessa kontroller ges till `VideoPlayer` med hjälp av ett config-objekt, som skickas till spelaren vid instansieringen. Som standard bildar varje komponent en hierarki av objekt, där elementet anges till spelarinstansen i trädets rot. När varje komponent skapas läggs den till i DOM på lämplig plats.

Varje komponent har ett namn, som är dess nyckel i config-objektet när objektet registreras. CSS-klassen för det underliggande DOM-elementet har formatet `vp-`-prefix som läggs till i komponentnamnet.

Komponenter kan utökas eller ersättas, deras konfiguration kan ändras och initiala egenskaper anges. På så sätt får du större kontroll över API-egenskaperna, CSS-klassnamnet och, eventuellt, komponentimplementeringens aspekter. Dessa alternativ kan användas för att anpassa funktioner och tillåta flera instanser av en komponent som kan formateras eller konfigureras individuellt.

Alla komponentinstanser kan nås med egenskapen `.behaviors`. Instanser kan aktiveras, inaktiveras, visas eller döljas. Men när instanserna väl har skapats kan dessa instanser inte tas bort.
