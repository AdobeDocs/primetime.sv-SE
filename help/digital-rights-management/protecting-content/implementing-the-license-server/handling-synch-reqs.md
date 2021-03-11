---
title: Hantera synkroniseringsbegäranden
description: Hantera synkroniseringsbegäranden
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Hantera synkroniseringsbegäranden {#handle-synchronization-requests}

Om en licens anger synkroniseringskrav [för synkronisering,](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) skickar klienten regelbundet synkroniseringsbegäranden till servern baserat på den frekvens som anges i licensen. Om du vill aktivera synkroniseringsmeddelanden anger du `SyncFrequencyRequirements` i en PlayRight.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* Om både klient och server har stöd för protokoll version 5 är begärande-URL:en &quot;License Server URL in metadata: + &quot; [!DNL /flashaccess/sync/v4]&quot;. I annat fall är begärande-URL:en &quot;License Server URL in metadata&quot; + &quot; [!DNL /flashaccess/sync/v3]&quot;

Synkroniseringsmeddelanden används för att synkronisera klientens tid med serverns tid. Om licenser är inbäddade i innehållet och inte behöver hämtas från en licensserver är det viktigt att synkronisera klientens tid för att förhindra att klientens klocka ändras för att kringgå licensens förfallotid.

Synkroniseringsmeddelanden kan också användas för att kommunicera klienttillståndsinformation till servern ( `getClientState()`) för återställningsidentifiering.

Se [Återställningsskydd](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection).
