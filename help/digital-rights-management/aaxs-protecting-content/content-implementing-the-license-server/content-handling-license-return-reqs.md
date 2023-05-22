---
title: Hantera licensreturbegäranden
description: Hantera licensreturbegäranden
copied-description: true
exl-id: c8813f7a-9a12-4c71-a945-cee73b6784fd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Hantera licensreturbegäranden{#handling-license-return-requests}

Om klientprogrammet behöver returnera en licens anropar det ActionScript-API:t för DRMManager.returnVoucher() för att initiera processen. Detta API kan fungera i läget directCommit eller i läget confirmFirst. Om värdet för directCommit är true kommer klienten att ta bort de lokala licenserna omedelbart utan att vänta på en bekräftelse från licensservern att den har fått en begäran om att returnera licenserna. Adobe Access-licensservern bör behandla begäran och skicka ett svar till klienten. Det är licensservern som avgör om licensservern faktiskt gör något med begäran (till exempel minskar antalet licenser för den angivna användaren).

* Klassen för begärandehanteraren är com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* Begäranmeddelandeklassen är com.adobe.flashaccess.sdk.protocol.licenserurn.LicenseReturnRequestMessage

Den lägsta version av Adobe Access SDK som krävs är version 5. begärande-URL:en blir &quot; `/flashaccess/lreturn/v5`&quot;. Som med domänavregistrering bör servern använda `getRequestPhase()` för att avgöra om kunden förhandsgranskar en licensretur.
