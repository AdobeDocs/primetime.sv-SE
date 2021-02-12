---
description: För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.
seo-description: För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.
seo-title: Annonsersättning för VAST- och VMAP-annonser
title: Annonsersättning för VAST- och VMAP-annonser
uuid: 7b44abf9-50cf-4e39-b594-ceb52208a865
translation-type: tm+mt
source-git-commit: cecc559480b9b52c412fefff4361603d6f14caf7
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# Lägg till reserv för VAST- och VMAP-annonser {#ad-fallback-for-vast-and-vmap-ads}

För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.

I specifikationen VAST/Digital Video Multiple Ad Playlist (VMAP) anges att för annonser där VAST-återgång är aktiverad, utlöser tomma annonser automatiskt användningen av reservannonser. När en VAST-annons är tom söker TVSDK efter en giltig ersättning för HLS-medietyp bland reservannonserna. När en VAST-annons i en wrapper har en ogiltig medietyp hanterar TVSDK den här annonsen som tom. Du kan konfigurera om TVSDK ska göra samma sak för annonser som är infogade i en VMAP. Mer information om funktionen VAST `fallbackOnNoAd` finns i [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## Definiera reservannonsbeteenden för VMAP-textbundna annonser {#define-fallback-ad-behavior-for-vmap-inline-ads}

Du kan aktivera reservfunktionen när en intern VMAP-fil innehåller en ogiltig medietyp.

1. Ange `fallbackOnInvalidCreative` som true om du vill att VMAP ska återställas när medietypen för en linjär/intern annons är ogiltig för HLS.

   Standardvärdet är false. Om en linjär annons misslyckas på grund av att den har en ogiltig medietyp, eller eftersom annonsen inte kan paketeras om, tillåter den här flaggan Primetime-annonsbeslut att följa samma reservbeteende som om annonsen var en tom VAST-wrapper.

   ```
   var auditudeMetadata:AuditudeSettings = new AuditudeSettings(); 
   auditudeMetadata.fallbackOnInvalidCreative = true;
   ```

## Annonsbeteende för VAST och VMAP {#ad-fallback-behavior-for-vast-and-vmap}

När Primetimes annonsbeslut påträffar en VAST-annons (creative) som är tom eller som har en medietyp som är ogiltig för HLS, utvärderas reservannonserna för att avgöra vad som ska returneras.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

I TVSDK är de enda giltiga medietyperna `application/x-shockwave-flash` (VPAID) och `application/x-mpegURL` (m3u8).

När det finns fristående reservannonser undersöker Primetime-modulen för annonsbeslut annonserna i följande ordning och returnerar den första annonsen med en giltig medietyp:

1. Om ompaketering är aktiverat behandlas den första förekomsten av en annons med en ogiltig medietyp som andra ogiltiga medietyper.

   Om ompaketering misslyckas gäller den här processen för ytterligare förekomster av annonsen.
1. Om TVSDK inte hittar några giltiga reservannonser returneras den ursprungliga annonsen med den ogiltiga medietypen.
1. Om en reservannons med en giltig MIME-typ returneras i stället för den ursprungliga annonsen, skickar Primetime-annonsbeslut felkoden 403 till VAST-fel-URL:en, om en sådan finns.
1. Om en reservannons är en wrapper och returnerar flera annonser returneras bara annonser med rätt medietyp.

>[!IMPORTANT]
>
>Det här beteendet är alltid aktiverat för annonser i VAST-omslutningar. För VAST-annonser som är infogade i en VMAP är beteendet inaktiverat som standard, men programmet kan aktivera det.