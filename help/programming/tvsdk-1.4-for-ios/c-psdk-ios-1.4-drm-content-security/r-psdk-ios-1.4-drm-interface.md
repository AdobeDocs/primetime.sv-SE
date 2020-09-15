---
description: Det viktigaste klientelementet i Primetimes DRM-system (Digital Rights Management) är DRM Manager.
seo-description: Det viktigaste klientelementet i Primetimes DRM-system (Digital Rights Management) är DRM Manager.
seo-title: Översikt över Primetime DRM-gränssnittet
title: Översikt över Primetime DRM-gränssnittet
uuid: 3aae7c7a-fd0c-430e-9018-fd72801ab778
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# Översikt över Primetime DRM-gränssnittet {#primetime-drm-interface-overview}

Du kan använda funktionerna i Primetime Digital Rights Management-systemet (DRM) för att ge säker åtkomst till ditt videoinnehåll. Du kan också använda DRM-lösningar från tredje part som ett alternativ till Adobe-integrerad Primetime DRM-lösning.

Kontakta din Adobe-representant för att få den senaste informationen om tillgängliga DRM-lösningar från tredje part.

Det viktigaste klientelementet i Primetimes DRM-system (Digital Rights Management) är DRM Manager.

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM ger ett skalbart och effektivt arbetsflöde för att implementera innehållsskydd i TVSDK-program. Du skyddar och hanterar rättigheterna till ditt videoinnehåll genom att skapa en licens för varje digital mediefil.

TVSDK stöder integrering av Primetime DRM som anpassade DRM-arbetsflöden. Detta innebär att ditt program måste implementera arbetsflödena för DRM-autentisering innan strömmen spelas upp med Flash DRMManager. MediaPlayer ger dig DRM-hanteraren för autentisering för att aktivera detta.

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

>[!TIP]
>
>När du refererar till DRM-skyddade resurs-URL:er i din iOS-app, `?faxs=1` måste frågesträngsparametern läggas till i (MBR)-URL:en på angiven nivå. Exempel:
>
>
```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>Frågesträngsparametern signalerar att innehållet är DRM-skyddat och utlöser DRM-dekrypteringsarbetsflödet i iOS TVSDK. `faxs=1` Du kan också lägga till taggen på webbadresser för DRM-skyddade HLS-resurser som är avsedda för andra plattformar. `faxs=1` det observeras som nödvändigt på iOS eller behandlas som icke-aktiv i spelare på andra plattformar.

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

Mer information om DRM finns i [Adobe Primetime DRM-dokumentationen](https://help.adobe.com/en_US/primetime/drm).

## Implementera Primetime DRM i ett TSVDK-program {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM är integrerat i TVSDK, vilket förenklar implementeringen av innehållsskydd i en TVSDK-applikation.

En översikt och information om hur du använder Primetime DRM för att implementera innehållsskydd i ett TVSDK-program finns i:

* [Adobe Primetime TVSDK-DRM Workflow (PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)