---
description: Ni kan hantera strömmar med livevideo och leverera alternativt innehåll under en strömavgång.
seo-description: Ni kan hantera strömmar med livevideo och leverera alternativt innehåll under en strömavgång.
seo-title: API-element för svart
title: API-element för svart
uuid: 263a8987-0c85-493a-9352-9605c877ba65
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# API-element för svart{#blackout-api-elements}

Ni kan hantera strömmar med livevideo och leverera alternativt innehåll under en strömavgång.

När en strömbrytning inträffar i en liveström använder spelaren händelsehanterare för att upptäcka strömmen och ge alternativt innehåll till de användare som inte är berättigade att titta på huvudströmmen. Spelaren känner av start- och slutpunkten för den utblinda perioden, växlar uppspelningen från huvudströmmen till en alternativ ström och växlar tillbaka till huvudströmmen när den utsläckta perioden är slut.

För att hantera strömavbrott i liveströmmar:

1. Konfigurera appen för att identifiera svarta out-taggar genom att prenumerera på svarta out-taggar i ett live-stream-manifest.

   TVSDK upptäcker inte ensam strömslutningstaggar. du måste prenumerera på utmattningstaggar för att få ett meddelande när taggarna påträffas under tolkningen av manifestfilen.
1. Skapa händelseavlyssnare för taggar som spelaren prenumererar på (i det här fallet PLAYBACK- och BLACKOUTS-taggar).

   När en tagg inträffar som spelaren har prenumererat på (till exempel en out-tagg) i antingen förgrunden (huvudinnehåll) eller bakgrundsströmmanifest (alternativt innehåll), skickar TVSDK en `TimedMetadataEvent` tagg och skapar en `TimedMetadataObject` för `TimedMetadataEvent`.

1. Implementera hanterare för tidsbestämda metadatahändelser för både förgrunds- och bakgrundsströmmarna.

   I de här hanterarna hämtar du start- och sluttider för utmörningsperioden från tidsbestämda metadatahändelseobjekt.
1. Skapa metoder för att växla innehåll i början och slutet av den svarta punkten.

   När utströmningsperioden börjar växlar du huvudinnehållet till bakgrunden och växlar det alternativa innehållet till huvudströmmen. Fortsätt att hämta och tolka det ursprungliga manifestet i bakgrunden och fortsätt att söka efter sluttaggen för utmörkning, så att spelaren kan återansluta till den ursprungliga strömmen när utsläckningen är slut.
1. Uppdatera icke sökbara intervall om det svarta området finns i DVR i uppspelningsströmmen.

   Spåra och hantera materialet `TimedMetadata` i bakgrundsströmmen genom att förbereda och uppdatera svärta ut icke sökbara intervall.

TVSDK innehåller API-element som är användbara när du implementerar utfall, inklusive metoder, metadata och meddelanden.

Du kan använda följande när du implementerar en svartpunkt i din spelare.

* **MediaPlayer**

   * `registerCurrentItemAsBackgroundItem` Sparar den inlästa resursen som bakgrundsresurs. Om `replaceCurrentResource` anropas efter den här metoden fortsätter TVSDK att hämta bakgrundsobjektets manifest tills du anropar `unregisterCurrentBackgroundItem`, `release`eller `reset`.

   * `unregisterCurrentBackgroundItem` Anger att bakgrundsobjektet ska vara null och stoppar hämtning och tolkning av bakgrundsmanifestet.

* **BlackoutMetadata** -

   En metadataklass som är specifik för strömavbrott.

   På så sätt kan du ställa in icke sökbara intervall (en array med `TimeRanges`) på TVSDK. TVSDK söker efter dessa intervall varje gång användaren söker. Om den är inställd och användaren söker i ett intervall som inte kan sökas tvingar TVSDK användaren till slutet av det intervall som inte går att söka i.

* **START HERE NEXT AdvertisingMetadata** Enable or disable preroll on a live stream by setting `enableLivePreroll` to true or false. Om värdet är false gör inte TVSDK något explicit annonsserveranrop för pre-roll-annonser före innehållsuppspelningen och spelar därför inte upp pre-roll. Detta påverkar inte mittrullarna. Standardvärdet är true.

* **MediaPlayer.BlackoutsEventListener**

   * `onTimedMetadataInBackgroundItem` - Skickas när identifierar en prenumerationstagg i bakgrundsmanifestet och en ny `TimedMetadata` instans förbereds. Instansen skickas `TimedMetadata` som en parameter.

   * `onBackgroundManifestFailed` - Skickas när mediespelaren helt inte kan läsa in bakgrundsmanifestet, det vill säga att alla strömmens URL returnerar antingen ett fel eller ett ogiltigt svar.

* **Meddelanden**

   * `BACKGROUND_MANIFEST_WARNING`

      * Kod: 204000
      * Typ: Varning
      * Fel vid hämtning av bakgrundsmanifest.