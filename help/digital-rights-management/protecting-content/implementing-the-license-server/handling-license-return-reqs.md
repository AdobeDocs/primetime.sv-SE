---
title: Hantera licensreturbegäranden
description: Hantera licensreturbegäranden
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Hantera licensreturbegäranden{#handle-license-return-requests}

Om klientprogrammet behöver returnera en licens anropar det ActionScript-API:t `DRMManager.returnVoucher()` för att initiera processen. Detta API kan fungera i ett `immediateCommit`-läge eller ett `confirmFirst`-läge. Om `immediateCommit` är inställt på `true` tar klienten bort de lokala licenserna omedelbart utan att vänta på bekräftelse från licensservern om att den har tagit emot en begäran om att returnera licenserna. Adobe Primetime DRM-licensservern bör behandla begäran och skicka ett svar till klienten. Om licensservern bearbetar begäran, t.ex. minskning av antalet licenser för en viss användare, avgörs av licensservern.

* Klassen för begärandehanteraren är `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

Minst `Adobe Primetime DRM` SDK-version som krävs är version 5; URL:en för begäran är [!DNL /flashaccess/lreturn/v5]. Precis som med domänavregistrering använder servern `getRequestPhase()` för att avgöra om klienten kan förhandsgranska licensreturer.
