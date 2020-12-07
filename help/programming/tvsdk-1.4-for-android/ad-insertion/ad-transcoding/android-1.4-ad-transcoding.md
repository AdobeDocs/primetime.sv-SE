---
description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas i innehållsströmmen för HTTP-direktuppspelning (HLS) eftersom deras videoformat inte är kompatibelt med HLS. Primetimes annonsinfogning och TVSDK kan som tillval försöka paketera om inkompatibla annonser i kompatibla M3U8-videor.
seo-description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas i innehållsströmmen för HTTP-direktuppspelning (HLS) eftersom deras videoformat inte är kompatibelt med HLS. Primetimes annonsinfogning och TVSDK kan som tillval försöka paketera om inkompatibla annonser i kompatibla M3U8-videor.
seo-title: Paketera inkompatibla annonser med Adobe Creative Repackaging Service
title: Paketera inkompatibla annonser med Adobe Creative Repackaging Service
uuid: eea3651f-2598-4efa-ba4d-dbd7afa7cb95
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Paketera inkompatibla annonser med Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas i innehållsströmmen för HTTP-direktuppspelning (HLS) eftersom deras videoformat inte är kompatibelt med HLS. Primetimes annonsinfogning och TVSDK kan som tillval försöka paketera om inkompatibla annonser i kompatibla M3U8-videor.

Annonser från olika tredjepartsleverantörer, t.ex. en annonsserver, en lagerpartner eller ett annonsnätverk, levereras ofta i inkompatibla format, t.ex. progressiv nedladdning av MP4.

När TVSDK först stöter på en inkompatibel annons ignorerar spelaren annonsen och skickar en begäran till den kreativa reparationstjänsten (CRS), som är en del av Primetime-annonsinfogningen, för att paketera om annonsen till ett kompatibelt format. CRS försöker generera M3U8-renderingar med flera bitar och lagrar dessa renderingar i Primetimes Content Delivery Network (CDN). Nästa gång TVSDK får ett annonssvar som pekar på den annonsen använder spelaren den HLS-kompatibla M3U8-versionen från CDN.

Om du vill aktivera den här valfria funktionen kontaktar du Adobe.

Mer information om CRS finns i [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Flera CDN-stöd för CRS och leverans{#multiple-cdn-support-for-crs-ad-delivery}

Standardscenariot för Creative Repackaging Service (CRS) är att använda ett CDN (Content Data Network), men du kan distribuera CRS-resurser på mer än ett CDN.

Du kan använda flera CDN av följande skäl:

* Ett krav på att skala upp för stora visningshändelser.
* Ett krav som matchar CDN-källan för CRS-resursen med CDN-källan för huvudinnehållet.

Du kan omvandla den standard-URL som tillhandahålls av CRS med hjälp av TVSDK URL Transformer API:er.

Här är API-tilläggen i TVSDK:

* `URLTransformer` Ett gränssnitt som beskriver de metoder som krävs för att omforma CRS- och URL:er som begärs av TVSDK. Applikationerna kan implementera det här gränssnittet och tillhandahålla implementeringar för de metoder som krävs.

* `DefaultURLTransformer` Den standardinstans av URL-transformatorn som skapas i TVSDK och som implementerar  `URLTransformer` gränssnittet. Program kan åsidosätta den här klassen eller lägga till en post-URL-omformningshanterare. Den här hanteraren är användbar när programmet vill göra ändringar i URL-begäran efter att standardomformningen har tillämpats.

* `NetworkConfiguration.setURLTransformer` En set-metod som anges i  `NetworkConfiguration` metadatainstansen för att ställa in  `URLTransformer` implementeringen.

>[!IMPORTANT]
>
>Appimplementeringarna måste kontrollera `URLTransformerInputType`-uppräkningen och endast transformera URL:er av typen `URLTransformerInputType.CRSCreative` för CRS.

I följande kodexempel visas hur ditt program kan ändra standardvärdkomponenten till en annan sträng (till exempel `cdn.mycrsdomain.com`):

```java
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
DefaultURLTransformer urlTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(new DefaultURLTransformer.URLTransformHandler() { 
    @Override 
    public String call(String url, URLTransformerInputType type) { 
        if (type == URLTransformerInputType.CRSCreative) { 
            try { 
                return url.replaceAll(new java.net.URI(url).getHost(), "cdn.mycrsdomain.com"); 
            } catch (URISyntaxException e) { 
            } 
        } 
        return url; 
    } 
}); 
   
networkConfiguration.setURLTransformer(urlTransformer); 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(), networkConfiguration);
```
