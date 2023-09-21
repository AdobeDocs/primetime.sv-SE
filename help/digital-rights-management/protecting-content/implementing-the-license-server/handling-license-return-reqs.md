---
title: Hantera licensreturbegäranden
description: Hantera licensreturbegäranden
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Hantera licensreturbegäranden{#handle-license-return-requests}

Om klientprogrammet behöver returnera en licens, anropas `DRMManager.returnVoucher()` ActionScript API för att initiera processen. Detta API kan fungera i en `immediateCommit` läge eller `confirmFirst` läge. If `immediateCommit` är inställd på `true`tar klienten sedan bort de lokala licenserna omedelbart utan att vänta på bekräftelse från licensservern att den har fått en begäran om att returnera licenserna. Adobe Primetime DRM-licensservern bör behandla begäran och skicka ett svar till klienten. Om licensservern bearbetar begäran, t.ex. minskning av antalet licenser för en viss användare, avgörs av licensservern.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

Minimivärdet `Adobe Primetime DRM` SDK-version som krävs är version 5. URL:en för begäran är [!DNL /flashaccess/lreturn/v5]&quot;. Precis som med domänavregistrering använder servern `getRequestPhase()` för att avgöra om kunden kan förhandsgranska en licensretur.
