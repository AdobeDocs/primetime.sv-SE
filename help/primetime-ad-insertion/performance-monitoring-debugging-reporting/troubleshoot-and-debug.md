---
title: Felsöka och felsöka
description: Felsöka och felsöka
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Felsöka och felsöka {#troubleshooting-debugging}

Primetime Ad Insertion har verktyg för att identifiera och diagnostisera problem som kan inträffa i alla faser av videoleverans, till exempel CDN-leveransfel, kreativa fel eller klientanslutningsfel.

Primetime Ad Insertion har stöd för utförlig loggning via [Bootstrap API-parameter](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` eller `ptdebug=AdCall` till bootstrap-URL. Loggar skickas till både HTTP-svarshuvuden och till Primetimes Ad Insertion-konsol. Den här parametern är endast avsedd för lokaliserad testning, inte för produktionsströmmar. Mer information om meddelandetyper när utförlig loggning är aktiverat finns i [ptdebug-loggningshändelser i utförlig loggning](verbose-logging.md#ptdebug-logging-events).

Primetime Ad Insertion kan också felsöka prestanda vid alla förfrågningar med rubriken X-ADBE-AI-X1, som kan användas för att mäta prestanda och annonsinfogningar vid varje given begäran. Det här begärandehuvudet är tillgängligt oavsett om utförlig loggning är aktiverat eller inte. Mer information finns i [Detaljrubriker: X-ADBE-PTAI-X1](debugging-headers.md).
