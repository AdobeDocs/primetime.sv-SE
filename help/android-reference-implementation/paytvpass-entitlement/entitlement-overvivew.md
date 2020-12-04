---
description: Entitlement Manager är den funktionshanterare som stöder implementeringen av Primetime-autentisering.
seo-description: Entitlement Manager är den funktionshanterare som stöder implementeringen av Primetime-autentisering.
seo-title: Tillståndshanteraren - översikt
title: Tillståndshanteraren - översikt
uuid: b33dfae3-a132-4215-9992-80cbf4c87a61
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Tillståndshanteraren - översikt {#entitlement-manager-overview}

Entitlement Manager är den funktionshanterare som stöder implementeringen av Primetime-autentisering.

## Funktionsöversikt

Primetimes autentiseringsintegrering med referensimplementeringen för Android Primetime SDK lägger till en ny funktionshanterare i programmet. Till skillnad från många andra funktionshanterare används *EntitlementManager på flera ställen i programmet*. Nedan ges en översikt över ändringar och tillägg som gjorts i referensimplementeringen för att ge stöd åt Primetime-autentisering:

### Klassen EntitlementManager

Klassen `EntitlementManager` hanterar all kommunikation med Primetimes SDK för autentisering, plus kapslar in den programlogik som krävs för berättigandearbetsflödena. Det publika API:t för `EntitlementManager` används av programmet för att initiera tillståndsarbetsflöden, medan gränssnittet `EntitlementMangerListener` innehåller en callback-funktion som programmet kan hantera `EntitlementManger`-händelser.

### EntitlementManger-återanrop

Referensimplementeringens huvudaktivitet, `CatalogActivity`, skapar en instans av `EntitlementManagerListener` och registrerar den med `EntitlementManager`. På så sätt kan `EntitlementManager` signalera att det behövs gränssnittsuppdateringar till resten av programmet. Återanropen inkluderar att visa/dölja en inläsningsdialogruta, visa statusdialogrutor, uppdatera behörighets- och autentiseringsikoner och starta videouppspelning vid lyckad auktorisering.

### Tillståndsdialogrutor

Klassen `EntitlementDialogFragment` genererar dialogmeddelanden baserat på berättigandestatusen som skickas till klasskonstruktorn. Den här klassen används för meddelanden om lyckade autentiseringar samt för alla felmeddelanden. I `CatalogActivity` visas dialogrutorna för tillstånd när den tar emot specifika händelser från `EntitlementManager`. Dessutom implementerar `CatalogActivity` gränssnittet `EntitlementDialogListener`, som innehåller callback-metoder som signalerar när en dialogruta stängs eller när användaren loggar ut från autentiseringstjänsten Primetime.

### Val och inloggning av innehållsleverantör

Under autentiseringen med Primetime-autentisering kan två nya aktiviteter, `MvpdPickerActivity` och `MvpdLoginActivity`, låta användaren välja sin innehållsleverantör och logga in. Båda dessa aktiviteter startas från `CatalogActivity` via `EntitlementManager`. Dessutom returnerar både `MvpdPickerActivity` och `MvpdLoginActivity` resultat till `CatalogActivity` och därför måste `CatalogActivity` åsidosätta metoden `Activity.onActivityResult`.

### Inloggningsknapp

Referensimplementeringens huvudaktivitet, `CatalogActivity`, innehåller en ny inloggningsknapp i åtgärdsfältet. Med knappen Logga in kan användaren initiera autentisering med Primetime-autentisering. Dessutom kan användaren initiera autentisering genom att välja en skyddad video för uppspelning. Inloggningsknappens ikon och text ändras beroende på användarens autentiseringsstatus, och `CatalogActivity` innehåller kod för att uppdatera knappens ikon och text när sidan uppdateras. Det gör du genom att anropa `CatalogActivity` när &lt;a0/> startas för att uppdatera användarens autentiseringsstatus.`EntitlementManager.checkAuthentication()`

### Innehållsberättigande

I `CatalogView` visas nya ikoner ovanpå innehållsikonen för att signalera användarens auktoriseringsstatus för innehållet. Om användaren till exempel har förbehörighet att visa en video visas en grön cirkel över innehållet. Om användaren inte har förbehörighet att visa videon visas en nyckelikon. Visningen av dessa ikoner hanteras i `ContentTileAdapter`, men uppdateringen av deras tillstånd initieras från `CatalogActivity` när ett återanrop i `EntitlementManagerListener` anropas.

### Uppspelning av innehåll

Videouppspelning kräver nu en auktoriseringskontroll av `EntitlementManager`. Anropet till `EntitlementManager.getAuthorization()` görs inom `CatalogView`. Om videon kräver auktorisering och användaren är auktoriserad startas `PlayerActivity` från `CatalogActivity`.

