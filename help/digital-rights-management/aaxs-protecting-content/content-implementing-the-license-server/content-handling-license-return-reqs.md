---
seo-title: Hantera licensreturbegäranden
title: Hantera licensreturbegäranden
uuid: d184faea-88cb-44f3-a253-e5314d577f17
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Hantera licensreturbegäranden{#handling-license-return-requests}

Om klientprogrammet behöver returnera en licens anropar det ActionScript-API:t för DRMManager.returnVoucher() för att initiera processen. Detta API kan fungera i läget directCommit eller i läget confirmFirst. Om värdet för directCommit är true kommer klienten att ta bort de lokala licenserna omedelbart utan att vänta på en bekräftelse från licensservern att den har fått en begäran om att returnera licenserna. Adobe Access-licensservern ska behandla begäran och skicka ett svar till klienten. Det är licensservern som avgör om licensservern faktiskt gör något med begäran (till exempel minskar antalet licenser för den angivna användaren).

* Klassen för begärandehanteraren är com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* Begäranmeddelandeklassen är com.adobe.flashaccess.sdk.protocol.licenserurn.LicenseReturnRequestMessage

Adobe Access SDK måste ha version 5; begärans URL är &quot; `/flashaccess/lreturn/v5`&quot;. Precis som med domänavregistrering bör servern använda `getRequestPhase()` för att avgöra om klienten förhandsgranskar en licensretur.
