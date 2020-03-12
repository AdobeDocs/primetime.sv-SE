---
seo-title: Använda översikten över klassen DRMManager
title: Använda översikten över klassen DRMManager
uuid: 71ce061b-75b6-4ab5-8bbd-cafe7c3e4592
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Använda klassen DRMManager {#using-the-drmmanager-class}

Använd klassen `DRMManager` för att hantera licenser och DRM-licensserversessioner i Primetime i program.

**Licenshantering**

När en enhet spelar upp skyddat innehåll hämtas och cachelagras den licens som krävs för att visa innehållet. Om innehållet sparas lokalt och licensen tillåter uppspelning offline, kan användaren visa innehållet i programmet utan någon nätverksanslutning. Med `DRMManager`hjälp av kan du cachelagra licensen i förväg. Programmet behöver inte skaffa den licens som krävs för att visa innehållet. Programmet kan till exempel hämta mediefilen och sedan hämta licensen medan användaren fortfarande är online.

Använd ett `DRMContentData` objekt om du vill läsa in en licens i förväg. Objektet innehåller URL:en till Primetimes DRM-licensserver som kan tillhandahålla licensen och beskriver om användarautentisering krävs. `DRMContentData` Med den här informationen kan du anropa `DRMManager` metoden för att hämta och cachelagra licensen `loadVoucher()` . Arbetsflödet för att förhandsladda licenser beskrivs mer ingående i *Förhandsladda licenser för uppspelning* offline.

**Sessionshantering**

Du kan också använda `DRMManager` för att autentisera användaren mot en Primetime DRM-licensserver och för att hantera beständiga sessioner. Anropa `DRMManager` `authenticate()` metoden för att upprätta en session med DRM-licensservern Primetime. När autentiseringen har slutförts skickar `DRMManager` objektet ett `DRMAuthenticationCompleteEvent` objekt. Det här objektet innehåller en sessionstoken. Du kan spara denna token för att upprätta framtida sessioner så att användaren inte behöver ange sina kontouppgifter. Skicka token till `setAuthenticationToken()` metoden för att skapa en ny autentiserad session. (Inställningarna för den server som genererade variabeln avgör tokens förfallodatum och andra attribut).

## Hantera DRMStatus-händelser {#handling-drmstatus-events}

Det `DRMManager` skickar ett `DRMStatusEvent` objekt när ett anrop till `loadVoucher()` metoden har slutförts. Om en licens hämtas har detail-egenskapen för event-objektet värdet: och egenskapen voucher `DRM.voucherObtained`innehåller `DRMVoucher` objektet. Om ingen licens hämtas har detail-egenskapen fortfarande värdet: `DRM.voucherObtained`; voucher-egenskapen är emellertid null. Det går inte att hämta en licens om du t.ex. använder `LoadVoucherSetting` licensen `localOnly` och det inte finns någon lokalt cachelagrad licens. Om `loadVoucher()` anropet inte slutförs korrekt, kanske på grund av ett autentiserings- eller kommunikationsfel, `DRMManager` skickar i stället ett `DRMErrorEvent` - eller `DRMAuthenticationErrorEvent` -objekt.

## Hantera DRMAuthenticationComplete-händelser{#handling-drmauthenticationcomplete-events}

Det `DRMManager` skickar ett `DRMAuthenticationCompleteEvent` objekt när en användare autentiseras via ett anrop till `authenticate()` metoden. Objektet `DRMAuthenticationCompleteEvent` innehåller en återanvändbar token som kan användas för att behålla användarautentiseringen i olika programsessioner. Skicka denna token till `DRMManager``setAuthenticationToken()` metod för att återupprätta sessionen. (Tokenskaparen anger tokenattribut som utgångsdatum. Adobe tillhandahåller inget API för granskning av tokenattribut.)

## Hantera DRMAuthenticationError-händelser{#handling-drmauthenticationerror-events}

Det `DRMManager` skickar ett `DRMAuthenticationErrorEvent` objekt när en användare inte kan autentiseras via ett anrop till `authenticate()` - eller `setAuthenticationToken()` -metoderna.