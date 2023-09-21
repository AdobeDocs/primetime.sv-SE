---
title: Hantera synkroniseringsbegäranden
description: Hantera synkroniseringsbegäranden
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Hantera synkroniseringsbegäranden{#handling-synchronization-requests}

. Om en licens anger synkroniseringskrav ([Krav för synkronisering](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)) skickar klienten regelbundet synkroniseringsbegäranden till servern baserat på den frekvens som anges i licensen. Om du vill aktivera synkroniseringsmeddelanden anger du SyncFrequencyRequirements i en PlayRight.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Om både klienten och servern stöder protokoll version 5 är förfrågnings-URL:en &quot;License Server URL in metadata: + &quot;/flashaccess/sync/v4&quot;. I annat fall är begärande-URL:en &quot;License Server URL in metadata&quot; + &quot;/flashaccess/sync/v3&quot;

Synkroniseringsmeddelanden används för att synkronisera klientens tid med serverns tid. Om licenser är inbäddade i innehållet och inte behöver hämtas från en licensserver är det viktigt att synkronisera klientens tid för att förhindra att klientens klocka ändras för att kringgå licensens förfallotid.

Synkroniseringsmeddelanden kan också användas för att kommunicera klienttillståndsinformation till servern ( `getClientState()`) för återställningsidentifiering. Se [Återställningsskydd](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).
