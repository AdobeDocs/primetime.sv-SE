---
description: Ni kan hantera strömmar med livevideo och leverera alternativt innehåll under en strömavgång.
title: API-element för svart
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# API-element för svart{#blackout-api-elements}

Ni kan hantera strömmar med livevideo och leverera alternativt innehåll under en strömavgång.

När en strömbrytning inträffar i en liveström använder spelaren händelsehanterare för att upptäcka strömmen och ge alternativt innehåll till de användare som inte är berättigade att titta på huvudströmmen. Spelaren känner av start- och slutpunkten för den utblinda perioden, växlar uppspelningen från huvudströmmen till en alternativ ström och växlar tillbaka till huvudströmmen när den utsläckta perioden är slut.

För att hantera strömavbrott i liveströmmar:

1. Konfigurera appen för att identifiera svarta out-taggar genom att prenumerera på svarta out-taggar i ett live-stream-manifest.

   TVSDK identifierar inte svartout-taggar separat. Du måste prenumerera på utmattningstaggar för att få ett meddelande när taggarna påträffas under parsning av manifestfiler.
1. Skapa händelseavlyssnare för taggar som spelaren prenumererar på (i det här fallet PLAYBACK- och BLACKOUTS-taggar).

   När en tagg inträffar som spelaren har prenumererat på (till exempel en tagg som gör att programmet tar slut) i antingen förgrundsströmmen (huvudinnehållet) eller bakgrundsströmmen (alternativt innehåll), skickar TVSDK en `TimedMetadataEvent` och skapar en `TimedMetadataObject` för `TimedMetadataEvent`.

1. Implementera hanterare för tidsbestämda metadatahändelser för både förgrunds- och bakgrundsströmmarna.

   I de här hanterarna hämtar du start- och sluttider för utmörningsperioden från tidsbestämda metadatahändelseobjekt.
1. Skapa metoder för att växla innehåll i början och slutet av den svarta punkten.

   När utströmningsperioden börjar växlar du huvudinnehållet till bakgrunden och växlar det alternativa innehållet till huvudströmmen. Fortsätt att hämta och tolka det ursprungliga manifestet i bakgrunden och fortsätt att söka efter sluttaggen för utmörkning, så att spelaren kan återansluta till den ursprungliga strömmen när utsläckningen är slut.
1. Uppdatera icke sökbara intervall om det svarta området finns i DVR i uppspelningsströmmen.

   Spåra och hantera `TimedMetadata` på bakgrundsströmmen genom att förbereda och uppdatera svärta ut icke sökbara intervall.

TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.

Du kan använda följande när du implementerar en svartpunkt i din spelare.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Sparar den inlästa resursen som bakgrundsresurs. If `replaceCurrentResource` anropas efter den här metoden fortsätter TVSDK att hämta bakgrundsobjektets manifest tills du anropar `unregisterCurrentBackgroundItem`, `release`, eller `reset`.

   * `unregisterCurrentBackgroundItem` Anger att bakgrundsobjektet ska vara null och stoppar hämtning och tolkning av bakgrundsmanifestet.

* **BlackoutMetadata** -

  En metadataklass som är specifik för strömavbrott.

  På så sätt kan du ange icke sökbara intervall (en array med `TimeRanges`) på TVSDK. TVSDK söker efter dessa intervall varje gång användaren söker. Om den är inställd och användaren söker i ett intervall som inte kan sökas tvingar TVSDK användaren till slutet av det intervall som inte går att söka i.

* **STARTA HÄR NÄSTA ANNONSMETOD** Aktivera eller inaktivera inledning i en liveström genom att ange `enableLivePreroll` till true eller false. Om värdet är false gör inte TVSDK något explicit annonsserveranrop för pre-roll-annonser före innehållsuppspelningen och spelar därför inte upp pre-roll. Detta påverkar inte mittrullarna. Standardvärdet är true.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Skickas när identifierar en prenumerationstagg i bakgrundsmanifestet och en ny `TimedMetadata` -instansen förbereds från den. The `TimedMetadata` -instansen skickas som en parameter.

   * `onBackgroundManifestFailed` - Skickas när mediespelaren helt inte kan läsa in bakgrundsmanifestet, det vill säga att alla strömmens URL returnerar antingen ett fel eller ett ogiltigt svar.

* **Meddelanden**

   * `BACKGROUND_MANIFEST_WARNING`

      * Kod: 204000
      * Typ: Varning
      * Fel vid hämtning av bakgrundsmanifest.
