---
description: För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.
keywords: nollängd och tom annons
title: Annonsersättning för VAST- och VMAP-annonser
exl-id: 1fc04cac-e83f-4c1f-bf7b-1cbcb2135d53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Översikt {#ad-fallback-for-vast-and-vmap-ads-overview}

För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.

I specifikationen VAST/Digital Video Multiple Ad Playlist (VMAP) anges att tomma annonser automatiskt aktiverar användning av reservannonser för annonser som har VAST-återgång aktiverat. När en VAST-annons är tom söker TVSDK efter en giltig ersättning för HLS-medietyp bland reservannonserna. När en VAST-annons i en wrapper har en ogiltig medietyp hanterar TVSDK den här annonsen som tom. Du kan konfigurera om TVSDK ska göra samma sak för annonser som är infogade i en VMAP. Mer information om VAST `fallbackOnNoAd` funktion, se [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Nolllängdsannonser** - När TVSDK stöter på ett VAST-svar som innehåller en annons med längden noll, eller en annonsbrytning utan annonser, utlöses AD_BREAK_START / AD_BREAK_COMPLETE-händelser för dessa reklamavbrott med längden noll. *Detta beteende gäller endast för VOD-strömmar.* TVSDK utlöser dessa händelser även när din app använder annonspolicyn SKIP.
>
>TVSDK gör det *not* Fire AD_BREAK_START / AD_BREAK_COMPLETE för liveströmmar, eller när en användare använder Trickplay eller försöker gå förbi annonsen med nollängd.
