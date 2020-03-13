---
description: För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.
keywords: zero length ad;empty ad
seo-description: För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.
seo-title: Annonsersättning för VAST- och VMAP-annonser
title: Annonsersättning för VAST- och VMAP-annonser
uuid: ecfeff31-b723-4a0d-99f2-48705a37b5f0
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Översikt {#ad-fallback-for-vast-and-vmap-ads-overview}

För annonser (eller kreatörer) som har återgångsregeln aktiverad för Digital Video Ad Serving Template (VAST) hanterar TVSDK en annons med en ogiltig medietyp som en tom annons och försöker använda återgångsannonser i stället. Du kan konfigurera vissa aspekter av reservbeteendet.

I specifikationen VAST/Digital Video Multiple Ad Playlist (VMAP) anges att tomma annonser automatiskt aktiverar användning av reservannonser för annonser som har VAST-återgång aktiverat. När en VAST-annons är tom söker TVSDK efter en giltig ersättning för HLS-medietyp bland reservannonserna. När en VAST-annons i en wrapper har en ogiltig medietyp hanterar TVSDK den här annonsen som tom. Du kan konfigurera om TVSDK ska göra samma sak för annonser som är infogade i en VMAP. Mer information om VAST- `fallbackOnNoAd` funktionen finns i [Digital Video Ad Serving Template (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Nolllängdsannonser** - När TVSDK stöter på ett VAST-svar som innehåller en annons med längden noll, eller en annonsbrytning utan annonser, utlöses AD_BREAK_START / AD_BREAK_COMPLETE-händelser för dessa annonsbrytningar med längden noll. *Detta beteende gäller endast för VOD-strömmar.* TVSDK utlöser dessa händelser även när din app använder annonspolicyn SKIP.
>
>TVSDK utlöser *inte* AD_BREAK_START / AD_BREAK_COMPLETE-händelser för liveströmmar, eller när en användare använder Trickplay eller försöker gå förbi annonsen med nollängd.

