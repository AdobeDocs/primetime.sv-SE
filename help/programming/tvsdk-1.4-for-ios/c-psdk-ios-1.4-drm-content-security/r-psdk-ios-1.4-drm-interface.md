---
description: Det viktigaste klientelementet i Primetimes DRM-system (Digital Rights Management) är DRM Manager.
title: Översikt över Primetime DRM-gränssnittet
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# Översikt över Primetime DRM-gränssnittet {#primetime-drm-interface-overview}

Du kan använda funktionerna i Primetime Digital Rights Management-systemet (DRM) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobe-integrerad Primetime DRM-lösning.

Kontakta din Adobe-representant för att få den senaste informationen om tillgängliga DRM-lösningar från tredje part.

Det viktigaste klientelementet i Primetimes DRM-system (Digital Rights Management) är DRM Manager.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM ger ett skalbart och effektivt arbetsflöde för att implementera innehållsskydd i TVSDK-program. Du skyddar och hanterar rättigheterna till ditt videoinnehåll genom att skapa en licens för varje digital mediefil.

TVSDK stöder integrering av Primetime DRM som anpassade DRM-arbetsflöden. Detta innebär att ditt program måste implementera arbetsflödena för DRM-autentisering innan strömmen spelas upp med Flashen DRMManager. MediaPlayer ger dig DRM-hanteraren för autentisering för att aktivera detta.

Mer information finns i DRM-exempelspelarkoden som ingår i TVSDK-paketet.

Detta är de viktigaste API-elementen för att arbeta med DRM:

* En referens i mediespelaren till DRM-hanterarobjektet som implementerar DRM-undersystemet:

  ```
  @property (readonly, nonatomic) DRMManager *drmManager
  ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK utfärdar en `PTMediaPlayerItemDRMMetadataChanged` när DRM-metadata ändras. Dessa metadata används som indata för nästan alla funktioner i `DRMManager` klassen.

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

Om den DRM-skyddade strömmen är kodad med flera bithastigheter (MBR), bör de DRM-metadata som används för variantspellistan vara samma som de metadata som används i alla bithastighetsströmmar.

>[!TIP]
>
>När du refererar till DRM-skyddade resurs-URL:er i ditt iOS-program, frågesträngsparametern `?faxs=1` måste läggas till i (MBR) M3U8-URL:en på angiven nivå. Till exempel:
>
>```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>The `faxs=1` frågesträngsparametern signalerar att innehållet är DRM-skyddat och utlöser DRM-dekrypteringsarbetsflödet i enlighet med detta i iOS TVSDK. Du kan också lägga till `faxs=1` -tagg på DRM-skyddade URL:er för HLS-resurser som är avsedda för andra plattformar. Den observeras enligt iOS eller behandlas som en icke-aktiv spelare på andra plattformar.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Mer information om DRM finns i [Adobe Primetime DRM-dokumentation](https://help.adobe.com/en_US/primetime/drm).

## Implementera Primetime DRM i ett TSVDK-program {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM är integrerat i TVSDK, vilket förenklar implementeringen av innehållsskydd i en TVSDK-applikation.

En översikt och information om hur du använder Primetime DRM för att implementera innehållsskydd i ett TVSDK-program finns i:

* [Adobe Primetime TVSDK-DRM-arbetsflöde (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
