---
description: Du kan använda mål-C-API:t för Primetime Player för att anpassa spelarens beteende.
seo-description: Du kan använda mål-C-API:t för Primetime Player för att anpassa spelarens beteende.
seo-title: Klasser för mediespelare
title: Klasser för mediespelare
uuid: 705c71b6-4e5e-46b5-a59d-13df977b04f2
translation-type: tm+mt
source-git-commit: b13f2d3f083a6ca333a4edba1c8d7261f7d448ad

---


# Klasser för mediespelare {#media-player-classes}

Du kan använda mål-C-API:t för Primetime Player för att anpassa spelarens beteende.

Dessa klasser beskriver din mediespelare och dess resurser.

| Klass | Beskrivning |
|---|---|
| PTABRControlParameters | Innehåller alla adaptiva parametrar för bithastighetskontroll. Följande parametrar stöds:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Standardimplementering av PTMediaPlayerClientFactoryin i TVSDK. Den innehåller instanserna availablePTOpportunityResolver, PTContentResolver och PTAdPolicySelector. |
| PTMediaPlayer | Definierar rotkomponenten för Primetime Player-ramverket.Program skapar en instans av den här klassen för att spela upp media. Den här komponenten skickar meddelanden som meddelar programmet om spelarens status när som helst. |
| PTMediaPlayerClientFactory | Protokoll som beskriver de metoder som en anpassad mediaspelarklientfabrik ska implementera för att tillhandahålla tillgängliga PTOpportunityResolver-, PTContentResolver- och PTAdPolicySelector-instanser. |
| PTMediaPlayerItem | Representerar ett visst ljud-video-medium. |
| PTMediaPlayerView | Hanterar visningskomponenten i Primetime Player-ramverket. |
| PTMediaProfile | Representerar profilen för en enskild ström i variantspellistan. |
| PTMediaSelectionOption | Representerar en audiovisuell medieresurs för olika språkpreferenser, tillgänglighetskrav eller anpassade programkonfigurationer. Giltiga alternativtyper:<ul><li>Undertexter (PTMediaSelectionOptionTypeSubtitle)</li><li>Alternativt ljud (PTMediaSelectionOptionTypeAudio)</li><li>Undertexter (PTMediaSelectionOptionTypeCC)</li><li>Odefinierad (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| klassen PTOpportunityResolver,protokollet PTOpportunityResolver | En klass som används för att bearbeta in-manifest-cues som ska användas som ersättning för annonseringsprocessen i Adobe Primetime. |
| PTOpportunityResolverDelegate | Protokoll som beskriver de metoder som den anpassade affärsmöjlighetslösaren (PTOpportunityResolver) ska använda för att kommunicera status för matchningen av affärsmöjligheten till delegaten. |
| PTSDK | Beskriver versionen av TVSDK och dess funktioner. |
| PTSDKConfig | Visar globala TVSDK-inställningar och tillåter ett program att prenumerera på anpassade HLS-taggar. |
| PTTextStyleRule | Definierar konstanter som representerar textformatsattributnycklar som utgör regelordlistan. |
