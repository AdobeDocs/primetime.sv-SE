---
description: För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.
title: Annonsersättning för VAST- och VMAP-annonser
exl-id: 8e33793c-d278-4c82-ad9b-7c6c7ee69cd2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Annonsersättning för VAST- och VMAP-annonser {#ad-fallback-for-vast-and-vmap-ads}

För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.

I specifikationen VAST/Digital Video Multiple Ad Playlist (VMAP) anges att för annonser där VAST-återgång är aktiverad, utlöser tomma annonser automatiskt användningen av reservannonser. När en VAST-annons är tom söker TVSDK efter en giltig ersättning för HLS-medietyp bland reservannonserna. När en VAST-annons i en wrapper har en ogiltig medietyp hanterar TVSDK den här annonsen som tom. Du kan konfigurera om TVSDK ska göra samma sak för annonser som är infogade i en VMAP. Mer information om VAST `fallbackOnNoAd` funktion, se [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definiera reservannonsbeteenden för VMAP-textbundna annonser {#section_D90BB3C6E539472EABF000C0F616DBE2}

Du kan aktivera reservfunktionen när en intern VMAP-fil innehåller en ogiltig medietyp.

1. Ange `FallbackOnInvalidCreativeEnabled` till `YES` för att få VMAP tillbaka när medietypen för en linjär/intern annons är ogiltig för HLS.

   >[!NOTE]
   >
   >Standardvärdet är NO. Om en linjär annons misslyckas på grund av att den har en ogiltig medietyp, eller eftersom annonsen inte kan paketeras om, tillåter den här flaggan Primetime-annonsbeslut att följa samma reservbeteende som om annonsen var en tom VAST-wrapper.

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## Annonsbeteende för VAST och VMAP {#section_5B6716CC49CC4C40964CFE9F122C57A6}

När Primetimes annonsbeslut påträffar en VAST-annons (creative) som är tom eller som har en medietyp som är ogiltig för HLS, utvärderas reservannonserna för att avgöra vad som ska returneras.

I TVSDK är den enda giltiga medietypen `application/x-mpegURL` (M3U8).

När det finns fristående reservannonser undersöker Primetime-modulen för annonsbeslut annonserna i följande ordning och returnerar den första annonsen med en giltig medietyp:

1. Om ompaketering är aktiverat behandlas den första förekomsten av en annons med en ogiltig medietyp som andra ogiltiga medietyper.

   Om ompaketering misslyckas gäller den här processen för ytterligare förekomster av annonsen.
1. Om TVSDK inte hittar några giltiga reservannonser returneras den ursprungliga annonsen med den ogiltiga medietypen.
1. Om en reservannons med en giltig MIME-typ returneras i stället för den ursprungliga annonsen, skickar Primetime-annonsbeslut felkoden 403 till VAST-fel-URL:en, om en sådan finns.
1. Om en reservannons är en wrapper och returnerar flera annonser returneras bara annonser med rätt medietyp.

>[!IMPORTANT]
>
>Det här beteendet är alltid aktiverat för annonser i VAST-omslutningar. För VAST-annonser som är infogade i en VMAP är beteendet inaktiverat som standard, men programmet kan aktivera det.
