---
description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas i innehållsströmmen för HTTP-direktuppspelning (HLS) eftersom deras videoformat inte är kompatibelt med HLS. Primetimes annonsinfogning och TVSDK kan som tillval försöka paketera om inkompatibla annonser i kompatibla M3U8-videor.
title: Paketera inkompatibla annonser med hjälp av Adobe Creative Repackaging Service (CRS)
exl-id: 7e1f9ffd-cd7e-488b-bbb7-f78e1623b697
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '303'
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
>* CRS 3.1 minimerar nätverksanrop avsevärt, vilket förbättrar videons starttid.
>


## Aktivera CRS i TVSDK-program {#enable-crs-in-tvsdk-applications}

Om du vill aktivera CRS i TVSDK-program måste du ange följande information i Auditude-inställningarna:

1. Aktivera CRS i `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
