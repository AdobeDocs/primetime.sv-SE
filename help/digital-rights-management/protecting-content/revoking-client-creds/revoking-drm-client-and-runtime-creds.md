---
title: Återkalla DRM-klient- och körningsreferenser
description: Återkalla DRM-klient- och körningsreferenser
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Återkalla DRM-klient- och körningsreferenser {#revoking-drm-client-and-runtime-credentials}

DRM-/runtime-versioner identifieras av säkerhetsnivå, versionsnummer och andra attribut, inklusive operativsystem och körningsmiljö. Om du vill begränsa vilka DRM-/körningsversioner som tillåts anger du modulbegränsningarna i en DRM-princip eller i en `HandlerConfiguration`. Modulbegränsningar kan omfatta en lägsta säkerhetsnivå och en lista över modulversioner som inte får utfärdas för en licens.

Se [Blockeringslista i DRM-klienter som inte har åtkomst till skyddat innehåll](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) om du vill ha information om de attribut som används för att identifiera en DRM/körningsmodul.

Om den lägsta säkerhetsnivån anges måste klientens version (som anges i maskintoken) vara större än eller lika med det angivna värdet.

Om en lista över undantagna versioner anges och klientens version matchar någon av versionsidentifierarna i listan, kommer klienten inte att kunna använda en rättighet som innehåller denna ModuleRequirements-instans. För att en modul ska matcha versionsinformationen måste alla parametrar som anges i versionsinformationen, förutom versionsversionen, exakt matcha modulernas värden. Versionsversionen matchar om klientmodulens värde är mindre än eller lika med värdet i versionsinformationen.

Om en överträdelse rapporteras med en viss DRM-klient eller körningsversion kan innehållsägaren och innehållsdistributören (som kör licensservern) konfigurera servern så att den inte utfärdar några licenser under en period då Adobe inte har någon korrigering tillgänglig. Detta kan konfigureras via `HandlerConfiguration` enligt beskrivningen ovan, eller genom att ändra alla DRM-principer. I det senare fallet kan du underhålla en uppdateringslista för DRM-principen och använda den för att kontrollera om en DRM-princip har uppdaterats eller återkallats.

Om du behöver en nyare version av Adobe Flash Player/Adobe AIR Runtime eller Adobe Content Protection Library (DRM-modulen) måste du uppdatera DRM-principerna.

Se [Uppdatera en princip med Java API](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

Sedan måste du skapa en DRM-principuppdateringslista eller ange begränsningar i `HandlerConfiguration` genom att anropa `HandlerConfiguration.setRuntimeModuleRequirements()` eller `HandlerConfiguration.setDRMModuleRequirements()`. När en användare begär en ny licens med det angivna blockeringslista aktiverat måste du installera de senaste körtiderna och biblioteken innan en licens kan utfärdas.

Se exempelkoden i [Uppdatera en princip med Java API - exempel på blocklistning av DRM- och körningsversioner](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) för ett exempel på blocklistning av DRM- och körningsversioner.
