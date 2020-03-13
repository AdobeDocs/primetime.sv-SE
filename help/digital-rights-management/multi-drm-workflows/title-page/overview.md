---
description: Du kan implementera flera DRM-lösningar för dina TVSDK-appar med Primetime DRM Cloud, som drivs av ExpressPlay. DRM-lösningarna inkluderar Apples FairPlay, Googles WideVM, Microsofts PlayReady och Primetime Access från Adobe.
seo-description: Du kan implementera flera DRM-lösningar för dina TVSDK-appar med Primetime DRM Cloud, som drivs av ExpressPlay. DRM-lösningarna inkluderar Apples FairPlay, Googles WideVM, Microsofts PlayReady och Primetime Access från Adobe.
seo-title: Översikt över flera DRM
title: Översikt över flera DRM
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Arbetsflöden för flera DRM {#multi-drm-workflows}

Du kan implementera flera DRM-lösningar för dina TVSDK-appar med Primetime DRM Cloud, som drivs av ExpressPlay. DRM-lösningarna inkluderar Apples FairPlay, Googles WideVM, Microsofts PlayReady och Primetime Access från Adobe.

## Översikt över flera DRM {#multi-drm-overview}

Adobe TVSDK stöder DRM-skydd med flera DRM-scheman. Adobe erbjuder *Primetime DRM Cloud, som drivs av ExpressPlay* , för paketering, licensiering och uppspelning av videoinnehåll på flera plattformar.

DRM-scheman som stöds är bland annat Adobes *Primetime Access* DRM (AXS) och inbyggda DRM-moduler på olika enheter, inklusive [WideVM](https://www.widevine.com) på Chrome och Android, [FairPlay](https://developer.apple.com/streaming/fps/) på Safari och iOS samt [PlayReady](https://www.microsoft.com/playready/) på Edge och XboxOne. Kontakta en Adobe-representant för att få information om vilka DRM-scheman som finns tillgängliga på dessa plattformar samt om schemalagda datum för framtida releaser.

TVSDK stöder DRM-licenser som utfärdas av alla licensservrar som använder dessa protokoll. Förutom stöd för flera DRM-lösningar erbjuder Adobe *Primetime DRM Cloud, som drivs av ExpressPlay* som en lösning där ExpressPlay driver licensservrarna för varje lösning. Detta kan förenkla installation och underhåll av DRM-licenser.

Om du vill använda *Primetime DRM Cloud, som drivs av ExpressPlay* för att implementera dina DRM-behov i TVSDK-appar, måste du först skaffa ett [ExpressPlay.com](https://www.expressplay.com) -konto. ExpressPlay ger möjlighet till licensiering för flera olika DRM-skyddssystem och erbjuder även andra tjänster, inklusive paketering och nyckelhantering.

Din Adobe-representant kommer till att börja med att skapa ditt ExpressPlay-konto. Sedan kan du konfigurera ditt konto och få de *kundautentiserare* som du ska använda i licenstokenbegäranden till ExpressPlay-servrarna.