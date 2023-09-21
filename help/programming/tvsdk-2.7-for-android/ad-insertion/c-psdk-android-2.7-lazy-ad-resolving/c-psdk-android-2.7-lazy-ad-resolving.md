---
description: Annonsupplösning och annonsinläsning kan orsaka en oacceptabel fördröjning för en användare som väntar på att uppspelningen ska starta. Funktionerna Lazy Ad Loading och Lazy Ad Resolving kan minska startfördröjningen.
keywords: Lazy;Annonslösningar;Annonsinläsning
title: Lazy ad resolving
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Ökning {#lazy-ad-resolving}

Annonsupplösning och annonsinläsning kan orsaka en oacceptabel fördröjning för en användare som väntar på att uppspelningen ska starta. Funktionerna Lazy Ad Loading och Lazy Ad Resolving kan minska startfördröjningen.

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
   1. TVSDK löser och läser in återstående annonser och placerar dem på tidslinjen när uppspelningen sker.

  Lazy Ad Resolving bygger på Lazy Ad Loading för ännu snabbare start. När TVSDK har placerat ut några annonser före filmningen flyttas spelaren till PREPARED-status och ytterligare annonser löses och placeras sedan på tidslinjen.

>[!IMPORTANT]
>
>Faktorer att tänka på när det gäller Lazy Ad Resolving:
>
>* Lazy Ad Resolving är aktiverat som standard. Om du inaktiverar det löses alla annonser innan uppspelningen startar.
>* Lazy Ad Resolving tillåter inte sökning eller tricks förrän alla annonser är lösta:
>
>    * Spelaren måste vänta på `kEventAdResolutionComplete` -händelse innan sökning eller tricks kan spelas upp.
>    * Om användaren försöker utföra sök- eller tricks-uppspelningsåtgärder medan annonserna fortfarande är lösta, kommer TVSDK att `kECLazyAdResolutionInProgress` fel.
>    * Spelaren bör vid behov uppdatera navigeringsfältet, *efter* som tar emot `kEventAdResolutionComplete` -händelse.
>
>* Lazy Ad Resolving är endast för VOD. Det fungerar inte med LIVE-strömmar.
>* Lazy Ad Resolving är inte kompatibel med *Direkt på* -funktion.
>
>  Mer information om Direkt på finns i Direkt på.
>
>* Lazy Ad Resolving resulterar i att uppspelningen startar mycket snabbare, men om en annonsbrytning inträffar under de första 60 sekunderna av uppspelningen kanske den inte går att matcha.
>* Lazy-annonsupplösningen påverkar inte pre-roll-annonser.
