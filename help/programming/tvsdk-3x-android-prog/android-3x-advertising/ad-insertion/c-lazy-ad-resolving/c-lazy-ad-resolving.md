---
description: Annonsupplösning och annonsinläsning kan orsaka en oacceptabel fördröjning för en användare som väntar på att uppspelningen ska starta. Funktionerna Lazy Ad Loading och Lazy Ad Resolving kan minska startfördröjningen. Lazy Ad Resolving har ändrats avsevärt i version 3.0. I Lazy Ad som lästes in före 3.0 delades annonsupplösningen upp i två steg, vilket löste endast för- och efterrullningar innan statusen"PREPARED" samt för medelrullar och efterrullningar efter statusen"PREPARED". Detta har ändrats och annonsbrytningar har nu lösts vid ett angivet intervall före positionen för annonsbrytningen.
keywords: Lazy;Annonslösningar;Annonsinläsning
title: Just-in-time Ad Resolving
exl-id: 7ce0dcac-859b-4570-a31b-4ea1e10ccf95
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Översikt {#just-in-time-ad-resolving-overview}

Annonsupplösning och annonsinläsning kan orsaka en oacceptabel fördröjning för en användare som väntar på att uppspelningen ska starta. Funktionerna Lazy Ad Loading och Lazy Ad Resolving kan minska startfördröjningen. Lazy Ad Resolving har ändrats avsevärt i version 3.0. I Lazy Ad som lästes in före 3.0 delades annonsupplösningen upp i två steg, vilket löste endast för- och efterrullningar innan statusen&quot;PREPARED&quot; samt för medelrullar och efterrullningar efter statusen&quot;PREPARED&quot;. Detta har ändrats och annonsbrytningar har nu lösts vid ett angivet intervall före positionen för annonsbrytningen.

* Grundläggande annonslösning och inläsningsprocess:

   1. TVSDK hämtar ett manifest (playlist) och *lösningar* alla annonser.
   1. TVSDK *laddar* alla annonser och placerar dem på tidslinjen.
   1. TVSDK flyttar spelaren till PREPARED-status och uppspelningen av innehåll börjar.

   Spelaren använder URL:erna i manifestet för att hämta annonsinnehållet (kreatörerna), ser till att annonsinnehållet är i ett format som TVSDK kan spela upp, och TVSDK placerar annonserna på tidslinjen. Denna grundläggande process för att lösa och läsa in annonser kan orsaka en orimligt lång fördröjning för en användare som väntar på att spela upp sitt innehåll, särskilt om manifestet innehåller flera annons-URL:er.

* *Lazy Ad Loading*:

   1. TVSDK hämtar en spellista och *lösningar* alla annonser.
   1. TVSDK *laddar* pre-roll-ads, flyttar spelaren till PREPARED-status och uppspelningen av innehåll börjar.
   1. TVSDK *laddar* de återstående annonserna och placerar dem på tidslinjen när uppspelningen sker.

   Den här funktionen förbättrar den grundläggande processen genom att ge spelaren statusen FÖRBEREDD innan alla annonser har lästs in.

* *Lazy Ad Resolving*:

   1. TVSDK hämtar spellistan.
   1. TVSDK löser och läser in alla förrollsannonser, flyttar spelaren till statusen PREPARED och uppspelningen av innehåll börjar.
   1. TVSDK löser problemet och var och en av de återstående annonsbrytningarna var för sig baserat på följande beräkning:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      Som standard är detta 5.0 + 30.0 + 6.0 sekunder (41 sekunder) för innehåll med en 6 sekunder lång måltid

   1. Om en annonsbrytning inträffar inom 10 sekunder från startpositionen kommer den att lösas tillsammans med annonser före förregistrering innan statusen FÖRBEREDD.

>[!IMPORTANT]
>
>**Faktorer att tänka på när det gäller Lazy Ad Resolving:**
>
>* Lazy Ad Resolving stöds bara för VOD-strömmar med lägena SERVER_MAP och MANIFEST_CUES.
>* Lazy Ad Resolving är inte aktiverat som standard. Om det är inaktiverat löses alla annonser i VOD-strömmar innan uppspelningen startar.
>* Lazy Ad Resolving är inte kompatibelt med funktionen Instant On. Mer information om Direkt på finns i Direkt på.
>* Med Lazy Ad Resolving löses den närmaste brytningen till sökpositionen under sökningen när du söker framåt över en annonsbrytning.
>* Om det finns flera annonsbrytningar samtidigt i Lazy Ad-lösningen (VMAP) kommer de att lösas samtidigt.
>* Vi rekommenderar inte att du minskar värdet för *setDelayAdLoadingTolerance() *under standardvärdet (5 sekunder). Om du gör det kan spelaren buffras i onödan.
>* Lazy Ad Resolving påverkar inte pre-roll-ads.
>* Lazy Ad Resolving stöds för närvarande av Auditude-Plugin. Vi rekommenderar att du inte anger *setDelayAdLoading* till true om du använder en anpassad lösare.
>

