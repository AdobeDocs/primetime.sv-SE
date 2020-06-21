---
seo-title: Återkalla DRM-klient- och körningsreferenser
title: Återkalla DRM-klient- och körningsreferenser
uuid: 8e36536a-8eed-4d27-8a5f-8d3219817e57
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Återkalla DRM-klient- och körningsreferenser {#revoking-drm-client-and-runtime-credentials}

DRM-/runtime-versioner identifieras av säkerhetsnivå, versionsnummer och andra attribut, inklusive operativsystem och körningsmiljö. Om du vill begränsa vilka DRM-/runtime-versioner som tillåts anger du modulbegränsningarna i en DRM-princip eller i en `HandlerConfiguration`. Modulbegränsningar kan omfatta en lägsta säkerhetsnivå och en lista över modulversioner som inte får utfärdas för en licens.

Se [Blocklista över DRM-klienter som inte har åtkomst till skyddat innehåll](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) för mer information om de attribut som används för att identifiera en DRM/runtime-modul.

Om den lägsta säkerhetsnivån anges måste klientens version (som anges i maskintoken) vara större än eller lika med det angivna värdet.

Om en lista över undantagna versioner anges och klientens version matchar någon av versionsidentifierarna i listan, kommer klienten inte att kunna använda en rättighet som innehåller denna ModuleRequirements-instans. För att en modul ska matcha versionsinformationen måste alla parametrar som anges i versionsinformationen, förutom versionsversionen, exakt matcha modulernas värden. Versionsversionen matchar om klientmodulens värde är mindre än eller lika med värdet i versionsinformationen.

Om en överträdelse rapporteras med en viss DRM-klient eller körningsversion kan innehållsägaren och innehållsdistributören (som kör licensservern) konfigurera servern att neka att utfärda licenser under en period då Adobe inte har någon korrigering tillgänglig. Detta kan konfigureras via `HandlerConfiguration` enligt beskrivningen ovan eller genom att ändra alla DRM-principer. I det senare fallet kan du underhålla en uppdateringslista för DRM-principen och använda den för att kontrollera om en DRM-princip har uppdaterats eller återkallats.

Om du behöver en nyare version av Adobe Flash Player/Adobe AIR Runtime eller Adobe Content Protection-biblioteket (DRM-modulen) måste du uppdatera DRM-principerna.

Se [Uppdatera en profil med Java API](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

Sedan måste du skapa en DRM-principuppdateringslista eller ange begränsningar i `HandlerConfiguration` genom att anropa `HandlerConfiguration.setRuntimeModuleRequirements()` eller `HandlerConfiguration.setDRMModuleRequirements()`. När en användare begär en ny licens med de angivna blocklistorna aktiverade måste du installera de senaste körtiderna och biblioteken innan en licens kan utfärdas.

Se exempelkoden i [Uppdatera en princip med Java API. Ett exempel på blocklistning av DRM- och körningsversioner](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) innehåller ett exempel på blocklistning av DRM- och körningsversioner.
