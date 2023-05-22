---
description: Du kan implementera flera DRM-lösningar för dina TVSDK-appar med Primetime DRM Cloud, som drivs av ExpressPlay. DRM-lösningarna omfattar Apple FairPlay, Google Widewin, Microsoft PlayReady och Primetime Access från Adobe.
title: Översikt över flera DRM
exl-id: 27614bb6-bfa6-445a-8fb5-a1b8af080bcc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Arbetsflöden för flera DRM {#multi-drm-workflows}

Du kan implementera flera DRM-lösningar för dina TVSDK-appar med Primetime DRM Cloud, som drivs av ExpressPlay. DRM-lösningarna omfattar Apple FairPlay, Google Widewin, Microsoft PlayReady och Primetime Access från Adobe.

## Översikt över flera DRM {#multi-drm-overview}

Adobe TVSDK stöder DRM-skydd med hjälp av flera DRM-scheman. Adobe erbjuder *Primetime DRM Cloud från ExpressPlay* för att leverera paketering, licensiering och uppspelning av videomaterial på flera plattformar.

Bland de DRM-scheman som stöds finns Adobe *Primetime-åtkomst* DRM (AAXS), liksom inbyggda DRM på olika enheter, inklusive [Widewin](https://www.widevine.com) på Chrome och Android, [FairPlay](https://developer.apple.com/streaming/fps/) på Safari och iOS, och [PlayReady](https://www.microsoft.com/playready/) på Edge och XboxOne. Kontakta en Adobe-representant för att få information om vilka DRM-system som finns tillgängliga på dessa plattformar samt om schemalagda datum för framtida releaser.

TVSDK stöder DRM-licenser som utfärdas av alla licensservrar som använder dessa protokoll. Förutom stöd för flera DRM-lösningar erbjuder Adobe *Primetime DRM Cloud från ExpressPlay* som en lösning där ExpressPlay hanterar licensservrarna för varje lösning. Detta kan förenkla installation och underhåll av DRM-licenser.

Används *Primetime DRM Cloud från ExpressPlay* för att implementera DRM-behoven i TVSDK-appar måste du först få en [ExpressPlay.com](https://www.expressplay.com) konto. ExpressPlay ger möjlighet till licensiering för flera olika DRM-skyddssystem och erbjuder även andra tjänster, inklusive paketering och nyckelhantering.

Din Adobe-representant kommer till att börja med att konfigurera ditt ExpressPlay-konto. Sedan kan du konfigurera ditt konto och få *kundautentiserare* som du ska använda i licensieringstokenbegäranden till ExpressPlay-servrar.
