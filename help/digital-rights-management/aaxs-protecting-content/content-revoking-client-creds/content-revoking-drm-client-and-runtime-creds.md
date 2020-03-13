---
seo-title: Återkalla DRM-klient- och körningsreferenser
title: Återkalla DRM-klient- och körningsreferenser
uuid: 774b8ac7-51bb-42fc-a05d-cfa718e24a81
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Återkalla DRM-klient- och körningsreferenser{#revoking-drm-client-and-runtime-credentials}

DRM-/runtime-versioner identifieras av säkerhetsnivå, versionsnummer och andra attribut, inklusive operativsystem och körningsmiljö. Om du vill begränsa vilka DRM-/runtime-versioner som tillåts anger du modulbegränsningarna i en profil eller i en `HandlerConfiguration`. Modulbegränsningar kan omfatta en lägsta säkerhetsnivå och en lista över modulversioner som inte får utfärdas för en licens. Se [Svartlista över DRM-klienter som inte har åtkomst till skyddat innehåll](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blacklist-drm-clients.md) för mer information om de attribut som används för att identifiera en DRM/körningsmodul.

Om den lägsta säkerhetsnivån anges måste klientens version (som anges i maskintoken) vara större än eller lika med det angivna värdet.

Om en lista över undantagna versioner anges och klientens version matchar någon av versionsidentifierarna i listan, kommer klienten inte att kunna använda en rättighet som innehåller denna ModuleRequirements-instans. För att en modul ska matcha versionsinformationen måste alla parametrar som anges i versionsinformationen, förutom versionsversionen, exakt matcha modulernas värden. Versionsversionen matchar om klientmodulens värde är mindre än eller lika med värdet i versionsinformationen.

Om en överträdelse rapporteras med en viss DRM-klient eller körningsversion kan innehållsägaren och innehållsdistributören (som kör licensservern) konfigurera servern att neka att utfärda licenser under en period då Adobe inte har någon korrigering tillgänglig. Detta kan konfigureras via `HandlerConfiguration` enligt beskrivningen ovan eller genom att ändra alla profiler. I det senare fallet kan du underhålla en principuppdateringslista och använda den för att kontrollera om en profil har uppdaterats eller återkallats.

Om du behöver en nyare version av Adobe® Flash® Player/Adobe® AIR® Runtime eller Adobe Content Protection-biblioteket (DRM-modulen) uppdaterar du profilerna så som de visas i [Uppdatera en profil med Java API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) och skapar en principuppdateringslista, eller anger begränsningar i `HandlerConfiguration` genom att anropa `HandlerConfiguration.setRuntimeModuleRequirements()` eller `HandlerConfiguration.setDRMModuleRequirements()`. När en användare begär en ny licens med dessa svartlistor aktiverade, måste de nyare körtiderna och biblioteken installeras innan en licens kan utfärdas. Ett exempel på svartlistning av DRM- och körningsversioner finns i exempelkoden i [Uppdatera en princip med Java API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
