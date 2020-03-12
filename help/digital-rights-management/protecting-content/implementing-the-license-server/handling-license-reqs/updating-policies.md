---
seo-title: Uppdaterar DRM-principer
title: Uppdaterar DRM-principer
uuid: 6f7a1432-88e4-499b-a008-6c8cf0e9c09b
translation-type: tm+mt
source-git-commit: d5986e9bc8689bf37abdf242a41aea5e768df754

---


# Uppdaterar DRM-principer {#updating-drm-policies}

Om DRM-profiler uppdateras efter att innehållet har paketerats, ska du tillhandahålla de uppdaterade DRM-profilerna till licensservern så att den uppdaterade versionen kan användas när en licens utfärdas. Om en licensserver har åtkomst till en databas för lagring av DRM-principer kan du hämta den uppdaterade DRM-principen från databasen och anropa `LicenseRequestMessage.setSelectedPolicy()` för att tillhandahålla den nya versionen av DRM-principen.

För licensservrar som inte är beroende av en central databas har SDK stöd för DRM-principuppdateringslistor. En uppdateringslista för en DRM-princip är en fil som innehåller en lista över uppdaterade eller återkallade DRM-principer. När en DRM-princip uppdateras genererar du en ny DRM-principuppdateringslista och skickar regelbundet listan till alla licensservrar. Skicka listan till SDK genom att ange `HandlerConfiguration.setPolicyUpdateList()`. Om det finns en uppdateringslista läser SDK den här listan när innehållsmetadata tolkas. `ContentInfo.getUpdatedPolicies()` innehåller de uppdaterade versionerna av DRM-principer som anges i metadata.

Se [Arbeta med DRM-principer](../../../protecting-content/working-policies-overview/working-with-policies.md) och [DRM-principuppdateringslistor](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)