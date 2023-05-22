---
title: Använda översikten över klassen DRMManager
description: Använda översikten över klassen DRMManager
copied-description: true
exl-id: 941a69fb-3085-45d6-9176-08ebb93cada4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Använda klassen DRMManager {#using-the-drmmanager-class}

Använd `DRMManager` klass för att hantera licenser och Primetime DRM-licensserversessioner i program.

**Licenshantering**

När en enhet spelar upp skyddat innehåll hämtas och cachelagras den licens som krävs för att visa innehållet. Om innehållet sparas lokalt och licensen tillåter uppspelning offline, kan användaren visa innehållet i programmet utan någon nätverksanslutning. Använda `DRMManager`kan du cacha licensen i förväg. Programmet behöver inte skaffa den licens som krävs för att visa innehållet. Programmet kan till exempel hämta mediefilen och sedan hämta licensen medan användaren fortfarande är online.

Använd en `DRMContentData` -objekt. The `DRMContentData` -objektet innehåller URL:en till Primetime DRM-licensservern som kan tillhandahålla licensen och beskriver om användarautentisering krävs. Med den här informationen kan du ringa `DRMManager` `loadVoucher()` metod för att hämta och cachelagra licensen. Arbetsflödet för att förhandsladda licenser beskrivs mer ingående i *Förinläsning av licenser för uppspelning offline*.

**Sessionshantering**

Du kan också använda `DRMManager` för att autentisera användaren mot en Primetime DRM-licensserver och för att hantera beständiga sessioner. Ring `DRMManager` `authenticate()` metod för att upprätta en session med Primetimes DRM-licensserver. När autentiseringen är klar `DRMManager` skickar en `DRMAuthenticationCompleteEvent` -objekt. Det här objektet innehåller en sessionstoken. Du kan spara denna token för att upprätta framtida sessioner så att användaren inte behöver ange sina kontouppgifter. Skicka token till `setAuthenticationToken()` metod för att upprätta en ny autentiserad session. (Inställningarna för den server som genererade variabeln avgör tokens förfallodatum och andra attribut).

## Hantera DRMStatus-händelser {#handling-drmstatus-events}

The `DRMManager` skickar en `DRMStatusEvent` objektet efter ett anrop till `loadVoucher()` metoden har slutförts. Om en licens hämtas har detail-egenskapen för event-objektet värdet: `DRM.voucherObtained`och egenskapen voucher innehåller `DRMVoucher` -objekt. Om ingen licens hämtas har detail-egenskapen fortfarande värdet: `DRM.voucherObtained`; voucher-egenskapen är emellertid null. Det går inte att hämta en licens om du t.ex. använder `LoadVoucherSetting` av `localOnly` och det finns ingen lokal cachelagrad licens. Om `loadVoucher()` anropet inte slutförs korrekt, kanske på grund av ett autentiserings- eller kommunikationsfel, kan `DRMManager` skickar en `DRMErrorEvent` eller `DRMAuthenticationErrorEvent` i stället.

## Hantera DRMAuthenticationComplete-händelser{#handling-drmauthenticationcomplete-events}

The `DRMManager` skickar en `DRMAuthenticationCompleteEvent` när en användare autentiseras via ett anrop till `authenticate()` -metod. The `DRMAuthenticationCompleteEvent` objektet innehåller en återanvändbar token som kan användas för att behålla användarautentiseringen i olika programsessioner. Skicka denna token till `DRMManager` `setAuthenticationToken()` metod för att återupprätta sessionen. (Tokenskaparen anger tokenattribut som utgångsdatum. Adobe har inget API för att undersöka tokenattribut.)

## Hantera DRMAuthenticationError-händelser{#handling-drmauthenticationerror-events}

The `DRMManager` skickar en `DRMAuthenticationErrorEvent` när en användare inte kan autentiseras via ett anrop till `authenticate()` eller `setAuthenticationToken()` metoder.
