---
description: Du kan ange om uppspelning ska tillåtas innan alla annonser har lästs in och placerats på tidslinjen. När du startar uppspelningen på det här sättet får tittaren snabbare åtkomst till huvudinnehållet. Den här funktionen gäller endast för live DVR och fungerar inte med, till exempel VOD-resurser.
seo-description: Du kan ange om uppspelning ska tillåtas innan alla annonser har lästs in och placerats på tidslinjen. När du startar uppspelningen på det här sättet får tittaren snabbare åtkomst till huvudinnehållet. Den här funktionen gäller endast för live DVR och fungerar inte med, till exempel VOD-resurser.
seo-title: Aktivera lazy och loading
title: Aktivera lazy och loading
uuid: ac7c8801-7fa2-4f17-b79c-c603b3236948
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Aktivera lat och läsa in{#enable-lazy-ad-loading}

Du kan ange om uppspelning ska tillåtas innan alla annonser har lästs in och placerats på tidslinjen. När du startar uppspelningen på det här sättet får tittaren snabbare åtkomst till huvudinnehållet. Den här funktionen gäller endast för live DVR och fungerar inte med, till exempel VOD-resurser.

1. Använd den booleska egenskapen `delayAdLoading` i `AdvertisingMetadata`.

   * När värdet är false väntar TVSDK tills alla annonser är lösta och placerade innan övergången till statusen PREPARED görs. Som standard är det false.
   * När värdet är true tolkar TVSDK bara de initiala annonserna och övergångarna till statusen PREPARED. De återstående annonserna löses och placeras under uppspelningen.

1. Om du även vill aktivera fördröjd och inläsning med Adobe Primetime annonsbeslut anger du `true` när du skapar `AuditudeSettings`.

   Klassen `AuditudeSettings` ärver den här egenskapen från `AdvertisingMetadata`, men ärver inte det aktuella värdet.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Om du exakt vill spegla annonser som tips i ett navigeringsfält lyssnar du efter `TimelineEvent`. `TIMELINE_UPDATED` och rita om rensningsfältet varje gång du får den här händelsen.

   När VoD-strömmar använder fördröjd och inläsning placeras inte alla annonser på tidslinjen när spelaren förbereds, så du måste rita om rensningsfältet explicit.

   TVSDK optimerar utskicket av den här händelsen för att minimera antalet gånger som du måste rita om rensningsfältet. Därför är antalet tidslinjehändelser inte relaterat till antalet annonsbrytningar som ska placeras på tidslinjen. Om du till exempel har fem annonsbrytningar kanske du inte får exakt fem händelser.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

