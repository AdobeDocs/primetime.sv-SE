---
description: 'Tabellen innehåller detaljerad information om meddelanden om intäktsoptimering. '
seo-description: 'Tabellen innehåller detaljerad information om meddelanden om intäktsoptimering. '
seo-title: Kod för intäktsoptimering
title: Kod för intäktsoptimering
translation-type: tm+mt
source-git-commit: df3d60874701383325be1afdd1ec5fe036f855f8
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# Kod för intäktsoptimering {#revenue-optimization-code}

I den här tabellen finns detaljerad information om INTÄKTOPTIMERINGSmeddelanden.

## Aktivera rapportering av intäktsoptimering {#enable-revenue-optimization-reporting}

Aktivera den här rapporteringen genom att använda PTMediaPlayer-API: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>De flesta informationsmeddelanden innehåller relevanta metadata, till exempel URL:en för resursen som inte kunde hämtas. Vissa meddelanden innehåller metadata som anger om problemet uppstod i huvudvideoinnehållet, i det alternativa ljudinnehållet eller i en annons.

| Code | Namn | Inre meddelande | Metadatanycklar | Kommentarer |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_REPORTING | Ingen | Se tabellen nedan för metadatanycklar baserade på olika händelser. | Ingen |

| Händelseinformation | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** skickas i TVSDK när MediaPlayer::replaceCurrentResource anropas. | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackaging Enabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** skickas i TVSDK när innehållet har förberetts och är klart för uppspelning. Den här händelsen skickas inte vid varje manifestöverföring - skickas endast vid den första inläsningen. | clientTimestamp, contentURL, contentType, event, isLive, clientID |
| **AD_OPPORTUNITY_GENERATED** Skickas i TVSDK när en affärsmöjlighet genereras. | clientTimestamp, event, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_START** Skickas i TVSDK när en affärsmöjlighet börjar matchas. | clientTimestamp, event, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** Skickas i TVSDK när en annonslösare anropar MediaPlayerClient::notifyFailed(). Behöver fylla i data | opportunityId, notificationAD |
| **AD_RESOURCE_LOAD** skickas när en annonsresurs hämtas av URL. responseStartTime:Unix-tidsstämpel för när begäran först startades. responseTotalTime:Total tid (i sekunder) som det tog för ett svar att läsas in. responseStatus:Statuskoden som påträffades när resursen hämtades. status:&quot;error&quot; eller&quot;success&quot; referenceAdId:Det refererande annons-ID som begärde hämtning av den här resursen (om sådan finns). referenceUrl:Den refererande URL som begärde hämtning av den här resursen. errorMessage:Om statusen är &quot;error&quot;, finns orsaken till felet här. | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referenceURL, referenceAdId |
| **AD_RESOURCE_LOAD_CRS** skickas i TVSDK när en CRS används på en resurs, samt svaret för m3u8. resourceType:always &quot;crs&quot;. responseStartTime:Unix-tidsstämpel för när begäran först startades. responseTotalTime:Total tid (i sekunder) som det tog för ett svar att läsas in. responseStatus:Statuskoden som påträffades när resursen hämtades. status:&quot;error&quot; eller&quot;success&quot;. errorMessage:Om statusen är &quot;error&quot;, finns orsaken till felet här. mediaFileUrl:Den ursprungliga mediefilens URL som markerades. mediaFileBitrate:Bithastigheten för den valda mediefilen. mediaFileMimeType: MIME-typen för den valda mediefilen. url:Den sista resurs-URL:en. | OpportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** Skickas i TVSDK efter att en adBreak placerats på tidslinjen. Den här händelsen inträffar en gång för varje annonsbrytning. proposedTime:Den tid då annonsbrytningen begärdes att placeras. actualTime:Den tid då annonsbrytningen faktiskt placerades. proposedDuration:Varaktigheten för den annonsbrytning som begärdes för infogning. För direktinnehåll är detta referenslängden. För VOD-innehåll är detta normalt -1. actualDuration:Den faktiska längden på den infogade annonsbrytningen. Beräknas som den sammanlagda längden för alla annonser, som definieras av deras respektive segmentvaraktighet, som läggs till eller ersätts på den ursprungliga strömmens tidslinje. proposedAds:Antalet annonser i den föreslagna reklambrytningen. totalAds:Antalet annonser som har placerats ut. annonser...n:De infogade annonserna infogas här. Hela annonsmanifestinformationen kan hämtas från AD_OPPORTUNITY_RESOLVE_PROCESS | OpportunityId, status, errorMessage, proposedTime, proposedDuration, actualTime, actualDuration, proposedAds, totalAds, ads_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_START** Skickas i TVSDK när en annons börjar spelas upp. | clientTimestamp, event, id, url, duration, type, opportunityId, clientId |
| **AD_PLAYBACK_COMPLETE** Skickas i TVSDK när en annons har slutfört uppspelningen. | clientTimestamp, event, id, url, duration, type, opportunityId, clientId |
| **ADBREAK_PLAYBACK_START** Skickas i TVSDK när en ADbreak startar uppspelningen. | clientTimestamp, event, opportunityId, duration, time, clientId |
| **ADBREAK_PLAYBACK_COMPLETE** Skickas i TVSDK när en ADbreak-uppspelning är klar. | clientTimestamp, event, opportunityId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** Skickas i TVSDK när något innehåll är klart. Detta kan inträffa om strömmen ersätts, spelaren försätts i ett feltillstånd, spelaren återställs eller innehållet faktiskt slutförs. Den här händelsen krävs för att spåra ett sessions-ID. | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_ERROR** skickas i TVSDK när en annons har ett fel som spelas upp (variantströmfel). | händelse, fel, tidsstämpel, manifestUrl, time, opportunityId, url |
