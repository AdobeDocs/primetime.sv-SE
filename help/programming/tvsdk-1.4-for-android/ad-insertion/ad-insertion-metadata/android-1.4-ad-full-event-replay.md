---
description: Full-event replay (FER) är en VOD-resurs som fungerar som en live/DVR-resurs, så programmet måste vidta åtgärder för att se till att annonserna placeras på rätt sätt.
title: Aktivera annonser i repriser vid helhändelse
exl-id: d6f7efc9-48f4-4101-a425-c354557cdd4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Aktivera annonser i repriser vid helhändelse{#enable-ads-in-full-event-replay}

Full-event replay (FER) är en VOD-resurs som fungerar som en live/DVR-resurs, så programmet måste vidta åtgärder för att se till att annonserna placeras på rätt sätt.

För direktsänt innehåll använder TVSDK metadata/cues i manifestet för att avgöra var annonserna ska placeras. Ibland liknar dock direktsänt eller linjärt innehåll VOD-innehåll. När live-innehåll är klart, till exempel, en `EXT-X-ENDLIST` -taggen läggs till i det aktiva manifestet. För HLS är `EXT-X-ENDLIST` -taggen betyder att strömmen är en VOD-ström. TVSDK kan inte automatiskt skilja den här strömmen från en vanlig VOD-ström för att korrekt infoga annonser.

Programmet måste informera TVSDK om innehållet är live eller VOD genom att ange `AdSignalingMode`.

För en FER-ström bör Adobe Primetime annonsbeslutsserver inte innehålla en lista över annonsbrytningar som måste infogas på tidslinjen innan uppspelningen startar. Detta är den typiska processen för VOD-innehåll. Om du anger ett annat signeringsläge läser TVSDK i stället alla referenspunkter från FER-manifestet och går till annonsservern för varje referenspunkt för att begära en annonsbrytning. Den här processen liknar live-/DVR-innehåll.

Förutom varje begäran som är associerad med en referenspunkt gör TVSDK en extra annonsbegäran för annonser före rullning.

1. Hämta det signeringsläge som ska användas från en extern källa, till exempel vCMS.
1. Skapa reklamrelaterade metadata.
1. Om standardbeteendet måste skrivas över anger du `AdSignalingMode` genom att använda `AdvertisingMetadata.setSignalingMode`.

   Giltiga värden är `DEFAULT, SERVER_MAP`och `MANIFEST_CUES`.

   Du måste ange annonssignaleringsläget innan du anropar `prepareToPlay`. När TVSDK börjar matcha och placera annonser på tidslinjen ignoreras ändringar av annonseringssigneringsläget. Ange läge när du skapar `AuditudeSettings` -objekt.

1. Fortsätt till uppspelningen.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->
