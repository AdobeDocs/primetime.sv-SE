---
description: Entitlement Manager är den funktionshanterare som stöder implementeringen av Primetime-autentisering.
seo-description: Entitlement Manager är den funktionshanterare som stöder implementeringen av Primetime-autentisering.
seo-title: Tillståndshanteraren - översikt
title: Tillståndshanteraren - översikt
uuid: b33dfae3-a132-4215-9992-80cbf4c87a61
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Tillståndshanteraren - översikt {#entitlement-manager-overview}

Entitlement Manager är den funktionshanterare som stöder implementeringen av Primetime-autentisering.

## Funktionsöversikt

Primetimes autentiseringsintegrering med referensimplementeringen för Android Primetime SDK lägger till en ny funktionshanterare i programmet. Till skillnad från många andra funktionshanterare används EntitlementManager *på flera ställen i programmet*. Nedan ges en översikt över ändringar och tillägg som gjorts i referensimplementeringen för att ge stöd åt Primetime-autentisering:

### Klassen EntitlementManager

Klassen hanterar all kommunikation med Primetimes SDK för autentisering, plus den programlogik som krävs för berättigandearbetsflödena. `EntitlementManager` Programmets publika API `EntitlementManager`används av programmet för att initiera tillståndsarbetsflöden, medan gränssnittet innehåller en callback-funktion som gör att programmet kan hantera `EntitlementMangerListener` `EntitlementManger` händelser.

### EntitlementManger-återanrop

Referensimplementeringens huvudsakliga aktivitet, `CatalogActivity`, skapar en instans av `EntitlementManagerListener` och registrerar den med `EntitlementManager`. På så sätt kan användaren `EntitlementManager` signalera att det behövs gränssnittsuppdateringar till resten av programmet. Återanropen inkluderar att visa/dölja en inläsningsdialogruta, visa statusdialogrutor, uppdatera behörighets- och autentiseringsikoner och starta videouppspelning vid lyckad auktorisering.

### Tillståndsdialogrutor

Klassen `EntitlementDialogFragment` genererar dialogrutemeddelanden baserat på berättigandestatusen som skickas till klasskonstruktorn. Den här klassen används för meddelanden om lyckade autentiseringar samt för alla felmeddelanden. Dialogrutorna för tillstånd `CatalogActivity` visas när den tar emot specifika händelser från `EntitlementManager`. Dessutom implementeras `CatalogActivity` `EntitlementDialogListener` gränssnittet, som innehåller callback-metoder som signalerar när en dialogruta stängs eller när användaren loggar ut från autentiseringstjänsten Primetime.

### Val och inloggning av innehållsleverantör

Under autentiseringen med Primetime-autentisering kan två nya aktiviteter `MvpdPickerActivity` och `MvpdLoginActivity`användaren välja sin innehållsleverantör och logga in. Båda dessa aktiviteter startas från `CatalogActivity` via `EntitlementManager`webben. Dessutom måste både `MvpdPickerActivity` - och `MvpdLoginActivity` returresultaten till `CatalogActivity` och därmed `CatalogActivity` åsidosätta `Activity.onActivityResult` metoden.

### Inloggningsknapp

Referensimplementeringens huvudaktivitet, `CatalogActivity`, innehåller en ny inloggningsknapp i åtgärdsfältet. Med knappen Logga in kan användaren initiera autentisering med Primetime-autentisering. Dessutom kan användaren initiera autentisering genom att välja en skyddad video för uppspelning. Inloggningsknappens ikon och text ändras beroende på användarens autentiseringsstatus, och den innehåller kod som `CatalogActivity` uppdaterar knappens ikon och text när sidan uppdateras. Det gör du genom att `CatalogActivity` uppdatera användarens autentiseringsstatus `EntitlementManager.checkAuthentication()` när programmet startas.

### Innehållsberättigande

I `CatalogView`fönstret visas nya ikoner ovanpå innehållsikonen för att signalera användarens auktoriseringsstatus för innehållet. Om användaren till exempel har förbehörighet att visa en video visas en grön cirkel över innehållet. Om användaren inte har förbehörighet att visa videon visas en nyckelikon. Visningen av de här ikonerna hanteras i `ContentTileAdapter`, men uppdateringen av deras tillstånd initieras från `CatalogActivity` när ett återanrop i `EntitlementManagerListener` anropas.

### Uppspelning av innehåll

Videouppspelning kräver nu en auktoriseringskontroll av `EntitlementManager`. Anropet som ska `EntitlementManager.getAuthorization()` göras i `CatalogView`. Om videon kräver behörighet och användaren är auktoriserad, `PlayerActivity` startas den från `CatalogActivity`.

