---
description: Full-event replay (FER) är en VOD-resurs som fungerar som en live/DVR-resurs, så programmet måste vidta åtgärder för att se till att annonserna placeras på rätt sätt.
seo-description: Full-event replay (FER) är en VOD-resurs som fungerar som en live/DVR-resurs, så programmet måste vidta åtgärder för att se till att annonserna placeras på rätt sätt.
seo-title: Aktivera annonser i repriser vid helhändelse
title: Aktivera annonser i repriser vid helhändelse
uuid: 70e463bd-332c-4f91-ac05-03e79c0939a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Aktivera annonser i repriser vid helaktivitet{#enable-ads-in-full-event-replay}

Full-event replay (FER) är en VOD-resurs som fungerar som en live/DVR-resurs, så programmet måste vidta åtgärder för att se till att annonserna placeras på rätt sätt.

För direktsänt innehåll använder TVSDK metadata/cues i manifestet för att avgöra var annonserna ska placeras. Ibland liknar dock direktsänt eller linjärt innehåll VOD-innehåll. När det aktiva innehållet är klart läggs till exempel en `EXT-X-ENDLIST`-tagg till i det aktiva manifestet. För HLS betyder taggen `EXT-X-ENDLIST` att strömmen är en VOD-ström. TVSDK kan inte automatiskt skilja den här strömmen från en vanlig VOD-ström för att korrekt infoga annonser.

Programmet måste tala om för TVSDK om innehållet är live eller VOD genom att ange `AdSignalingMode`.

För en FER-ström bör Adobe Primetime annonsbeslutsserver inte innehålla en lista över annonsbrytningar som måste infogas på tidslinjen innan uppspelningen startar. Detta är den typiska processen för VOD-innehåll. Om du anger ett annat signeringsläge läser TVSDK i stället alla referenspunkter från FER-manifestet och går till annonsservern för varje referenspunkt för att begära en annonsbrytning. Den här processen liknar live-/DVR-innehåll.

Förutom varje begäran som är associerad med en referenspunkt gör TVSDK en extra annonsbegäran för annonser före rullning.

1. Hämta det signeringsläge som ska användas från en extern källa, till exempel vCMS.
1. Skapa reklamrelaterade metadata.
1. Om standardbeteendet måste skrivas över anger du `AdSignalingMode` med `AdvertisingMetadata.setSignalingMode`.

   Giltiga värden är `DEFAULT, SERVER_MAP` och `MANIFEST_CUES`.

   Du måste ange annonssignaleringsläget innan du anropar `prepareToPlay`. När TVSDK börjar matcha och placera annonser på tidslinjen ignoreras ändringar av annonseringssigneringsläget. Ange läge när du skapar `AuditudeSettings`-objektet.

1. Fortsätt till uppspelningen.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

