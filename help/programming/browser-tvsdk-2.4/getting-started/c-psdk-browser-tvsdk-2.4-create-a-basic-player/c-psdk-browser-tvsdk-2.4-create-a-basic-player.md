---
description: Om du vill använda Browser TVSDK måste du skapa och konfigurera en grundspelare. Om du vill spela upp videoinnehåll kan du skapa en grundläggande spelare på två sätt med webbläsarens TVSDK eller med gränssnittets ramverk.
seo-description: Om du vill använda Browser TVSDK måste du skapa och konfigurera en grundspelare. Om du vill spela upp videoinnehåll kan du skapa en grundläggande spelare på två sätt med webbläsarens TVSDK eller med gränssnittets ramverk.
seo-title: Grundläggande spelare
title: Grundläggande spelare
uuid: 44a27458-be12-452f-92b9-3cef79439257
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Översikt {#basic-player-overview}

Om du vill använda Browser TVSDK måste du skapa och konfigurera en grundspelare. Om du vill spela upp videoinnehåll kan du skapa en grundläggande spelare på två sätt: med webbläsarens TVSDK, eller med gränssnittsramverket.

## Använda webbläsarens TVSDK {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Använd de API:er som finns i webbläsarens TVSDK direkt för att koda videospelaren. SDK ger dig ramverk och verktyg samt en referensspelare att arbeta utifrån.

>[!TIP]
>
>Om du vill se detta fungera i en referensspelare ska du inte ange några attribut med `videoDiv`.

## Använda UI-ramverket {#section_AE02384CFEF64A448C108232AB62A9FF}

Den här modulen används för att skapa instanser av spelaren, där varje instans är bunden till ett DOM-element (document object model) som tillhandahålls av anroparen. Förutom att ha en instans av Browser TVSDK är varje spelarinstans värd för ett antal kontroller som utgör användargränssnittet för spelaren.

Genomförandet av varje kontroll består av två aspekter:

* An `HTMLElement`, som är den visuella representationen av komponenten på skärmen
* A `Behavior`, som hanterar `HTMLElement` och tillhandahåller ett API för interaktioner

Information om dessa kontroller tillhandahålls till `VideoPlayer` spelaren med hjälp av ett config-objekt, som skickas till spelaren när den instansieras. Som standard bildar varje komponent en hierarki av objekt, där elementet anges till spelarinstansen i trädets rot. När varje komponent skapas läggs den till i DOM på lämplig plats.

Varje komponent har ett namn, som är dess nyckel i config-objektet när objektet registreras. CSS-klassen för det underliggande DOM-elementet är formaterad som ett `vp-` prefix som läggs till i komponentnamnet.

Komponenter kan utökas eller ersättas, deras konfiguration kan ändras och initiala egenskaper anges. På så sätt får du större kontroll över API-egenskaperna, CSS-klassnamnet och, eventuellt, komponentimplementeringens aspekter. Dessa alternativ kan användas för att anpassa funktioner och tillåta flera instanser av en komponent som kan formateras eller konfigureras individuellt.

Alla komponentinstanser kan nås med `.behaviors` egenskapen. Instanser kan aktiveras, inaktiveras, visas eller döljas. Men när instanserna väl har skapats kan dessa instanser inte tas bort.
