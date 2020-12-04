---
description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas i innehållsströmmen för HTTP-direktuppspelning (HLS) eftersom deras videoformat inte är kompatibelt med HLS. Primetimes annonsinfogning och TVSDK kan som tillval försöka paketera om inkompatibla annonser i kompatibla M3U8-videor.
seo-description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas i innehållsströmmen för HTTP-direktuppspelning (HLS) eftersom deras videoformat inte är kompatibelt med HLS. Primetimes annonsinfogning och TVSDK kan som tillval försöka paketera om inkompatibla annonser i kompatibla M3U8-videor.
seo-title: Paketera inkompatibla annonser med hjälp av Adobe Creative Repackaging Service (CRS)
title: Paketera inkompatibla annonser med hjälp av Adobe Creative Repackaging Service (CRS)
uuid: ef542d13-6d52-4429-8a1e-0af2df236f12
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Paketera inkompatibla annonser med hjälp av Adobe Creative Repackaging Service (CRS) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas i innehållsströmmen för HTTP-direktuppspelning (HLS) eftersom deras videoformat inte är kompatibelt med HLS. Primetimes annonsinfogning och TVSDK kan som tillval försöka paketera om inkompatibla annonser i kompatibla M3U8-videor.

Annonser från olika tredjepartsleverantörer, t.ex. en annonsserver, en lagerpartner eller ett annonsnätverk, levereras ofta i inkompatibla format, t.ex. det progressiva MP4-nedladdningsformatet.

När TVSDK först stöter på en inkompatibel annons ignorerar spelaren annonsen och skickar en begäran till den kreativa reparationstjänsten (CRS), som är en del av Primetime-annonsinfogningen, för att paketera om annonsen till ett kompatibelt format. CRS försöker generera flera M3U8-renderingar av annonsen med bithastighet och lagrar dessa renderingar i Primetime Content Delivery Network (CDN). Nästa gång TVSDK får ett annonssvar som pekar på den annonsen använder spelaren den HLS-kompatibla M3U8-versionen från CDN.

Om du vill aktivera den här valfria CRS-funktionen kontaktar du Adobe.

>[!NOTE]
>
>För kunder med CRS version 3.0 (och tidigare) har följande ändringar förbättrats både vad gäller säkerhet och prestanda:
>
>* CRS 3.1 fortsätter med `https:` om innehållet som packas om använder `https:`. Detta minskar vissa spelares potential att presentera osäkert innehåll.
   >
   >
* CRS 3.1 minimerar nätverksanrop avsevärt, vilket förbättrar videons starttid.

>



Mer information om CRS finns i [Creative Packaging Service (CRS)](../../../../../dynamic-ad-insertion/creative-repackaging-service/crs-overview.md).

## Aktivera CRS i TVSDK-program {#enable-crs-in-tvsdk-applications}

Om du vill aktivera CRS i TVSDK-program måste du ange följande information i Auditude-inställningarna:

1. Aktivera CRS i `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
