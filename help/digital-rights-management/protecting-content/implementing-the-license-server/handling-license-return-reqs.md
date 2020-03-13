---
seo-title: Hantera licensreturbegäranden
title: Hantera licensreturbegäranden
uuid: 994df5af-476a-4ee8-b371-8900241be83d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Hantera licensreturbegäranden{#handle-license-return-requests}

Om klientprogrammet behöver returnera en licens anropar det ActionScript-API:t för att starta processen `DRMManager.returnVoucher()` . Detta API kan fungera i ett `immediateCommit` läge eller ett `confirmFirst` läge. Om `immediateCommit` är inställt på `true`tar klienten bort de lokala licenserna omedelbart utan att vänta på en bekräftelse från licensservern att den har tagit emot en begäran om att returnera licenserna. DRM-licensservern för Adobe Primetime bör behandla begäran och skicka ett svar till klienten. Om licensservern bearbetar begäran, t.ex. minskning av antalet licenser för en viss användare, avgörs av licensservern.

* Klassen för begäranhanteraren är `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* Begärandemeddelandeklassen är `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

Den lägsta `Adobe Primetime DRM` SDK-version som krävs är version 5. begärans URL är &quot; [!DNL /flashaccess/lreturn/v5]&quot;. Precis som med domänavregistrering använder servern `getRequestPhase()` för att avgöra om klienten kan förhandsgranska en licensretur.
