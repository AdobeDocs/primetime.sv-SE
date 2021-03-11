---
title: Uppdaterar principer
description: Uppdaterar principer
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Uppdaterar principer {#updating-policies}

Om profiler uppdateras efter att innehållet har paketerats, ska du tillhandahålla de uppdaterade profilerna till licensservern så att den uppdaterade versionen kan användas när en licens utfärdas. Om din licensserver har åtkomst till en databas för att lagra profiler kan du hämta den uppdaterade principen från databasen och ringa `LicenseRequestMessage.setSelectedPolicy()` för att ange den nya versionen av profilen.

För licensservrar som inte är beroende av en central databas har SDK stöd för principuppdateringslistor. En principuppdateringslista är en fil som innehåller en lista över uppdaterade eller återkallade principer. När en profil uppdateras genererar du en ny principuppdateringslista och skickar regelbundet ut listan till alla licensservrar. Skicka listan till SDK genom att ange `HandlerConfiguration.setPolicyUpdateList()`. Om det finns en uppdateringslista läser SDK den här listan när innehållsmetadata analyseras. `ContentInfo.getUpdatedPolicies()` innehåller uppdaterade versioner av profiler som anges i metadata.

Se [Arbeta med principer](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) och [Listor för principuppdatering.](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
