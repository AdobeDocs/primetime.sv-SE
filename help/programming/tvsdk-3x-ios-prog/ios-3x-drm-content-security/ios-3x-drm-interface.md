---
description: Du kan använda funktionerna i Primetimes DRM-system (Digital Rights Management) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobes integrerade Primetime DRM-lösning.
keywords: DRM;DASH;HLS
seo-description: Du kan använda funktionerna i Primetimes DRM-system (Digital Rights Management) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobes integrerade Primetime DRM-lösning.
seo-title: Översikt över Primetime DRM-gränssnittet
title: Översikt över Primetime DRM-gränssnittet
uuid: 5e794147-cc58-448c-b8ec-065e80ef01fd
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Översikt över Primetime DRM-gränssnittet {#primetime-drm-interface-overview}

Du kan använda funktionerna i Primetimes DRM-system (Digital Rights Management) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobes integrerade Primetime DRM-lösning.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Fråga din Adobe-representant om den senaste informationen om att det finns DRM-lösningar från tredje part.

Det viktigaste klientelementet i Primetimes DRM-system (Digital Rights Management) är DRM Manager.

Primetime DRM ger ett skalbart och effektivt arbetsflöde för att implementera innehållsskydd i TVSDK-program. Du skyddar och hanterar rättigheterna till ditt videoinnehåll genom att skapa en licens för varje digital mediefil.

TVSDK stöder integrering av Primetime DRM som anpassade DRM-arbetsflöden. Det innebär att programmet måste implementera arbetsflödena för DRM-autentisering innan strömmen spelas upp med Flash DRMManager. MediaPlayer ger dig DRM-hanteraren för autentisering för att aktivera detta.

Se exempelkoden för DRM som ingår i TVSDK-paketet.

Detta är de viktigaste API-elementen för att arbeta med DRM:

* En referens i mediespelaren till DRM-hanterarobjektet som implementerar DRM-undersystemet:

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK skickar ett `PTMediaPlayerItemDRMMetadataChanged` meddelande när DRM-metadata ändras. Dessa metadata används som indata för nästan alla funktioner i `DRMManager` klassen.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Om den DRM-skyddade strömmen är kodad med flera bithastigheter (MBR), bör de DRM-metadata som används för variantspellistan vara samma som de metadata som används i alla bithastighetsströmmar.

[!TIP] {prioritet=&quot;high&quot;}

När du refererar till DRM-skyddade resurs-URL:er i din iOS-app, `?faxs=1` måste frågesträngsparametern läggas till i (MBR)-URL:en på angiven nivå. Exempel:

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

Frågesträngsparametern signalerar att innehållet är DRM-skyddat och utlöser DRM-dekrypteringsarbetsflödet i iOS TVSDK. `faxs=1` Du kan också lägga till taggen på webbadresser för DRM-skyddade HLS-resurser som är avsedda för andra plattformar. `faxs=1` det observeras som nödvändigt på iOS eller behandlas som icke-aktiv i spelare på andra plattformar.

## Implementera Primetime DRM i ett TSVDK-program {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM är integrerat i TVSDK, vilket förenklar implementeringen av innehållsskydd i en TVSDK-applikation.

En översikt och information om hur du använder Primetime DRM för att implementera innehållsskydd i ett TVSDK-program finns i:

* [Adobe Primetime TVSDK-DRM Workflow (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)