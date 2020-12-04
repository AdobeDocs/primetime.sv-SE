---
description: Att ställa in principer är en process för att ange villkor för när och hur en användare får spela upp skyddat videoinnehåll.
seo-description: Att ställa in principer är en process för att ange villkor för när och hur en användare får spela upp skyddat videoinnehåll.
seo-title: Ställa in profiler
title: Ställa in profiler
uuid: 2d2672ce-5ed4-4868-aa5e-0a9e21a809b3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Ställa in profiler{#setting-policies}

Att ställa in principer är en process för att ange villkor för när och hur en användare får spela upp skyddat videoinnehåll.

En princip skapas som en del av din licenstokenbegäran. (Se [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) om du vill se ett exempel med Widewidget).

När en kunds kod på serversidan har fastställt att den kommer att utfärda en licens (baserat på berättigandekontroller, geopositionering eller annan nödvändig information), begär den en token och *i token* anger den obligatoriska `securityLevel`, `hdcpOutputControl` och `licenseDuration`. Det är alternativen på kundsidan för en global politik. Andra DRM-lösningar erbjuder liknande metoder, men detaljerna skiljer sig åt i de olika fallen och beskrivs närmare i de enskilda arbetsflödena.

>[!NOTE]
>
>Adobe innehåller ett exempel på en referensserver som visar hur du implementerar en egen tillståndsserver/storefront: [Referensserver: Exempel på ExpressPlay-tillståndsserver (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

