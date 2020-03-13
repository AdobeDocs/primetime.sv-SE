---
seo-title: Uppdaterar principer
title: Uppdaterar principer
uuid: f6686c8b-bedf-4ec5-a14e-f03326519f89
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uppdaterar principer {#updating-policies}

Om profiler uppdateras efter att innehållet har paketerats, ska du tillhandahålla de uppdaterade profilerna till licensservern så att den uppdaterade versionen kan användas när en licens utfärdas. Om din licensserver har åtkomst till en databas för att lagra profiler kan du hämta den uppdaterade principen från databasen och ringa `LicenseRequestMessage.setSelectedPolicy()` för att ange den nya versionen av profilen.

För licensservrar som inte är beroende av en central databas har SDK stöd för principuppdateringslistor. En principuppdateringslista är en fil som innehåller en lista över uppdaterade eller återkallade principer. När en profil uppdateras genererar du en ny principuppdateringslista och skickar regelbundet ut listan till alla licensservrar. Skicka listan till SDK genom att ange `HandlerConfiguration.setPolicyUpdateList()`. Om det finns en uppdateringslista läser SDK den här listan när innehållsmetadata analyseras. `ContentInfo.getUpdatedPolicies()` innehåller uppdaterade versioner av profiler som anges i metadata.

Se [Arbeta med profiler](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) och listor [med principuppdateringar.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
