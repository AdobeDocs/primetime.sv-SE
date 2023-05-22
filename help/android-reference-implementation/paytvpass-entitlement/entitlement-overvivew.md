---
description: Entitlement Manager är den funktionshanterare som stöder implementeringen av Primetime-autentisering.
title: Tillståndshanteraren - översikt
exl-id: a66e131e-283f-4378-b834-7cfa887b3ec9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Tillståndshanteraren - översikt {#entitlement-manager-overview}

Entitlement Manager är den funktionshanterare som stöder implementeringen av Primetime-autentisering.

## Funktionsöversikt

Primetimes autentiseringsintegrering med referensimplementeringen för Android Primetime SDK lägger till en ny funktionshanterare i programmet. Till skillnad från många andra funktionshanterare *EntitlementManager används på flera ställen i programmet*. Nedan ges en översikt över ändringar och tillägg som gjorts i referensimplementeringen för att ge stöd åt Primetime-autentisering:

### Klassen EntitlementManager

The `EntitlementManager` -klassen hanterar all kommunikation med Primetimes SDK för autentisering, plus kapslar in den programlogik som krävs för berättigandearbetsflödena. The `EntitlementManager`Programmets publika API används av programmet för att initiera tillståndsarbetsflöden, medan `EntitlementMangerListener` -gränssnittet innehåller en återanropsmekanism som programmet kan hantera `EntitlementManger` händelser.

### EntitlementManger-återanrop

Referensprogrammets huvudverksamhet, `CatalogActivity`, skapar en instans av `EntitlementManagerListener` och registrerar det med `EntitlementManager`. På det här sättet `EntitlementManager` kan signalera att det behövs gränssnittsuppdateringar till resten av programmet. Återanropen inkluderar att visa/dölja en inläsningsdialogruta, visa statusdialogrutor, uppdatera behörighets- och autentiseringsikoner och starta videouppspelning vid lyckad auktorisering.

### Tillståndsdialogrutor

The `EntitlementDialogFragment` klassen genererar dialogmeddelanden baserat på berättigandestatusen som skickas till klasskonstruktorn. Den här klassen används för meddelanden om lyckade autentiseringar samt för alla felmeddelanden. The `CatalogActivity` visar dialogrutorna för tillstånd när den tar emot specifika händelser från `EntitlementManager`. Dessutom är `CatalogActivity` implementerar `EntitlementDialogListener` gränssnitt, som innehåller återkopplingsmetoder som signalerar när en dialogruta stängs eller när användaren loggar ut från Primetimes autentiseringstjänst.

### Val och inloggning av innehållsleverantör

Under autentiseringen med Primetime-autentisering finns två nya aktiviteter, `MvpdPickerActivity` och `MvpdLoginActivity`, låter användaren välja sin innehållsleverantör och logga in. Båda dessa aktiviteter startas från `CatalogActivity` via `EntitlementManager`. Dessutom är båda `MvpdPickerActivity` och `MvpdLoginActivity` returnera resultaten till `CatalogActivity` och `CatalogActivity` måste åsidosätta `Activity.onActivityResult` -metod.

### Inloggningsknapp

Referensprogrammets huvudverksamhet, `CatalogActivity`, innehåller en ny inloggningsknapp i åtgärdsfältet. Med knappen Logga in kan användaren initiera autentisering med Primetime-autentisering. Dessutom kan användaren initiera autentisering genom att välja en skyddad video för uppspelning. Inloggningsknappens ikon och text ändras beroende på användarens autentiseringsstatus, och `CatalogActivity` innehåller kod för att uppdatera knappens ikon och text när sidan uppdateras. För att göra detta, när `CatalogActivity` startar, anropar `EntitlementManager.checkAuthentication()` för att uppdatera användarens autentiseringsstatus.

### Innehållsberättigande

I `CatalogView`visas nya ikoner ovanpå innehållsikonen för att signalera användarens auktoriseringsstatus för innehållet. Om användaren till exempel har förbehörighet att visa en video visas en grön cirkel över innehållet. Om användaren inte har förbehörighet att visa videon visas en nyckelikon. Visningen av dessa ikoner hanteras i `ContentTileAdapter`, men uppdateringen av deras tillstånd initieras från `CatalogActivity` när ett återanrop finns i `EntitlementManagerListener` anropas.

### Uppspelning av innehåll

Videouppspelning kräver nu en auktoriseringskontroll av `EntitlementManager`. Samtalet till `EntitlementManager.getAuthorization()` inträffar inom `CatalogView`. Om videon kräver behörighet och användaren är auktoriserad, `PlayerActivity` startas från `CatalogActivity`.
