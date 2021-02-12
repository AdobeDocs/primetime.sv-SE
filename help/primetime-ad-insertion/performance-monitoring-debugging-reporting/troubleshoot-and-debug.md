---
title: Felsöka och felsöka
description: null
translation-type: tm+mt
source-git-commit: 242b5a2875ebc0e0020296ce9489dd54438b5ad0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Felsök och felsök {#troubleshooting-debugging}

Primetime Ad Insertion har verktyg för att identifiera och diagnostisera problem som kan inträffa i alla faser av videoleverans, till exempel CDN-leveransfel, kreativa fel eller klientanslutningsfel.

Primetime Ad Insertion stöder utförlig loggning via [API-parametern ](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` eller `ptdebug=AdCall` till bootstrap-URL:en. Loggar skickas till både HTTP-svarshuvuden och till Primetimes Ad Insertion-konsol. Den här parametern är endast avsedd för lokaliserad testning, inte för produktionsströmmar. Mer information om meddelandetyper när utförlig loggning är aktiverat finns i [ptdebug-loggningshändelser i utförlig loggning](verbose-logging.md#ptdebug-logging-events).

Primetime Ad Insertion kan också felsöka prestanda vid alla förfrågningar med rubriken X-ADBE-AI-X1, som kan användas för att mäta prestanda och annonsinfogningar vid varje given begäran. Det här begärandehuvudet är tillgängligt oavsett om utförlig loggning är aktiverat eller inte. Mer information finns i [Utförliga rubriker: X-ADBE-PTAI-X1](debugging-headers.md).
