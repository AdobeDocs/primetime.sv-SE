---
description: Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.
seo-description: Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.
seo-title: Infoga annonser
title: Infoga annonser
uuid: 6e31cae5-7363-454f-82dd-e03c1e34cd3f
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---


# Infoga annonser {#insert-ads}

Annonsinfogningen åtgärdar annonser för video-on-demand (VOD), för liveströmning och för linjär direktuppspelning med annonsspårning och annonsuppspelning. TVSDK skickar de begärda förfrågningarna till annonsservern, tar emot information om annonser för det angivna innehållet och placerar annonserna i innehållet i faser.

En *`ad break`* innehåller en eller flera annonser som spelas upp i sekvens. TVSDK infogar annonser i huvudinnehållet som medlemmar i en eller flera annonsbrytningar.

>[!TIP]
>
>Om annonsen innehåller fel ignorerar TVSDK annonsen.

## Lös och infoga VOD-annonser {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK har stöd för flera användningsfall för VOD-annonsering och -matchning och infogning.

* Inläggning av annonser i förväg, där annonser infogas i början av innehållet.
* Annonsinfogning mellan rullar, där minst en annons infogas mitt i innehållet.
* Infogning av annonser efter rullning, där minst en annons läggs till i slutet av innehållet.

TVSDK löser annonserna, infogar annonserna på platser som definieras av annonsservern och beräknar den virtuella tidslinjen innan uppspelningen startar. När uppspelningen har startats kan inga ändringar göras, t.ex. annonser som infogas eller infogade annonser som tas bort.

## Lös och infoga live och linjär annonsering {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK stöder flera användningsfall för dynamisk och linjär annonsupplösning och infogning.

* Inläggning av annonser i förväg, där minst en annons infogas i början av innehållet.
* Annonsinfogning mellan rullar, där minst en annons infogas mitt i innehållet.

TVSDK löser annonserna och infogar annonserna när en referenspunkt påträffas i den aktiva eller linjära strömmen. Som standard stöder TVSDK följande kommandon som giltiga annonsmarkörer när annonser löses och placeras:

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

Dessa markörer kräver att metadatafältet är `DURATION` i sekunder och referensens unika ID. Exempel:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Mer information om ytterligare tips finns i [Prenumerera på anpassade taggar](../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-custom-tags-subscribe.md).

## Spåra klientannons {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK spårar automatiskt annonser för VOD och live/linjär direktuppspelning.

Meddelanden används för att informera programmet om annonsens förlopp, inklusive information om när en annons börjar och när den slutar.

## Implementera en tidig radbrytning {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

För annonsinfogning live-strömmar kan du behöva avsluta en annonsbrytning innan alla annonser i pausen spelas upp tills de är klara.

Här är några exempel på en snabb radbrytning:

* Annonsens varaktighet vid vissa sportevenemang.

   Även om en standardlängd anges måste annonsbrytningen avslutas om spelet återupptas innan pausen är slut.
* En nödsignal under en annonsbrytning i en liveström.

Möjligheten att avsluta en annonsbrytning tidigt identifieras med en anpassad tagg i manifestet som kallas&quot;splice-in&quot; eller en cue-in-tagg. TVSDK tillåter att programmet prenumererar på dessa delningstaggar för att ge möjlighet till delning.

* Så här använder du taggen `#EXT-X-CUE-IN` som en möjlighet att dela upp och implementerar en tidig radbrytning:

   1. Prenumerera på taggen.

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Lägg till den inledande affärsmöjlighetslösaren.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Så här delar du samma tagg för delning och delning:

1. Om programmet delar samma cue för att indikera cue-out/splice-out och cue-in/splice-in, utökar `PTDefaultAdOpportunityResolver` och implementerar `preparePlacementOpportunity` metoden.

   >[!TIP]
   >
   >I följande kod antas att programmet har en implementering för `isCueInOpportunity` metoden.

   ```
   - (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
   { 
         if ([self isCueInOpportunity:timedMetadata]) 
         { 
               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
           } 
           else 
           { 
               return [super preparePlacementOpportunity:timedMetadata]; 
         } 
   }
   ```

1. Registrera den utökade lösaren för affärsmöjlighet på `PTDefaultMediaPlayerClientFactory` instansen.

```
   // self.player is the PTMediaPlayer instance created for content and ad playback 
       PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
             
   // Clear existing resolver and register the new opportunity resolver 
   [clientFactory clearOpportunityResolvers]; 
   [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
```
