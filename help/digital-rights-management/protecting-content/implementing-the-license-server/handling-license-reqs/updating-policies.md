---
title: Uppdaterar DRM-principer
description: Uppdaterar DRM-principer
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Uppdaterar DRM-principer {#updating-drm-policies}

Om DRM-profiler uppdateras efter att innehållet har paketerats, ska du tillhandahålla de uppdaterade DRM-profilerna till licensservern så att den uppdaterade versionen kan användas när en licens utfärdas. Om en licensserver har åtkomst till en databas för lagring av DRM-principer kan du hämta den uppdaterade DRM-principen från databasen och ringa `LicenseRequestMessage.setSelectedPolicy()` för att tillhandahålla den nya versionen av DRM-principen.

För licensservrar som inte är beroende av en central databas har SDK stöd för DRM-principuppdateringslistor. En uppdateringslista för en DRM-princip är en fil som innehåller en lista över uppdaterade eller återkallade DRM-principer. När en DRM-princip uppdateras genererar du en ny DRM-principuppdateringslista och skickar regelbundet listan till alla licensservrar. Skicka listan till SDK genom att ange `HandlerConfiguration.setPolicyUpdateList()`. Om det finns en uppdateringslista läser SDK den här listan när innehållsmetadata tolkas. `ContentInfo.getUpdatedPolicies()` innehåller de uppdaterade versionerna av DRM-principer som anges i metadata.

Se [Arbeta med DRM-principer](../../../protecting-content/working-policies-overview/working-with-policies.md) och [Uppdateringslistor för DRM-princip](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
