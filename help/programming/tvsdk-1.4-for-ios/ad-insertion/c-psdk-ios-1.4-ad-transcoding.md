---
description: Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas i innehållsströmmen för HTTP-direktuppspelning (HLS) eftersom deras videoformat inte är kompatibelt med HLS. Primetimes annonsinfogning och TVSDK kan som tillval försöka paketera om inkompatibla annonser i kompatibla M3U8-videor.
title: Paketera inkompatibla annonser med Adobe Creative Repackaging Service
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Paketera inkompatibla annonser med Adobe Creative Repackaging Service{#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

Vissa tredjepartsannonser (eller andra kreatörer) kan inte sammanfogas i innehållsströmmen för HTTP-direktuppspelning (HLS) eftersom deras videoformat inte är kompatibelt med HLS. Primetimes annonsinfogning och TVSDK kan som tillval försöka paketera om inkompatibla annonser i kompatibla M3U8-videor.

Annonser från olika tredjepartsleverantörer, t.ex. en annonsserver, en lagerpartner eller ett annonsnätverk, levereras ofta i inkompatibla format, t.ex. progressiv nedladdning av MP4.

När TVSDK först stöter på en inkompatibel annons ignorerar spelaren annonsen och skickar en begäran till den kreativa reparationstjänsten (CRS), som är en del av Primetime-annonsinfogningen, för att paketera om annonsen till ett kompatibelt format. CRS försöker generera M3U8-renderingar med flera bitar och lagrar dessa renderingar i Primetimes Content Delivery Network (CDN). Nästa gång TVSDK får ett annonssvar som pekar på den annonsen använder spelaren den HLS-kompatibla M3U8-versionen från CDN.

Om du vill aktivera den här valfria funktionen kontaktar du Adobe.

Mer information om CRS finns i [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## Flera CDN-funktioner för CRS och leverans {#section_900FDDA5454143718F1EB4C9732C8E1C}

Standardscenariot för Creative Repackaging Service (CRS) är att använda ett CDN (Content Data Network), men du kan distribuera CRS-resurser på mer än ett CDN.

Du kan använda flera CDN av följande skäl:

* Ett krav på att skala upp för stora visningshändelser.
* Ett krav som matchar CDN-källan för CRS-resursen med CDN-källan för huvudinnehållet.

Du kan omvandla den standard-URL som tillhandahålls av CRS med hjälp av TVSDK URL Transformer API:er.

Här är API-tilläggen i TVSDK:

* `PTURLTransformer` Ett protokoll som beskriver de metoder som krävs för att omforma CRS- och URL:er som begärs av TVSDK. Applikationerna kan implementera det här protokollet och tillhandahålla implementeringar för de metoder som krävs.

* `PTDefaultURLTransformer` Den standardinstans av URL-transformatorn som skapas i TVSDK och som implementerar `PTURLTransformer` -protokoll. Program kan åsidosätta den här klassen eller lägga till en post-URL-omformningshanterare. Den här hanteraren är användbar när programmet vill göra ändringar i URL-begäran efter att standardomformningen har tillämpats.

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` En set-metod som anges på `PTNetworkConfiguration` metadatainstans för att ange `PTURLTransformer` implementering.

>[!IMPORTANT]
>
>Appimplementeringarna måste kontrollera om `PTURLTransformerInputType` uppräkning och endast transformera URL:er av typen `PTURLTransformerInputTypeCRSCreative` för CRS.

I följande kodexempel visas hur ditt program kan ändra standardvärdkomponenten till en annan sträng (till exempel `cdn.mycrsdomain.com`):

```
// The sample code below uses Non-ARC code 
PTNetworkConfiguration *networkConfiguration = [[[PTNetworkConfiguration alloc] init] autorelease]; 
   
PTDefaultURLTransformer *defaultTransformer = [[[PTDefaultURLTransformer alloc] init] autorelease]; 
    [defaultTransformer addPostURLTransformHandler:^NSString *(NSString *url, PTURLTransformerInputType type) { 
        if (type == PTURLTransformerInputTypeCRSCreative) { 
            return [url stringByReplacingOccurrencesOfString:[NSURL URLWithString:url].host  
              withString:@"cdn.mycrsdomain.com"]; 
        } 
            return url; 
    }]; 
  
[networkConfiguration setURLTransformer:defaultTransformer]; 
   
// metadata is the PTMetadata instance set on a PTMediaPlayerItem instance. 
[metadata setMetadata:[self getNetworkConfiguration] forKey:PTNetworkConfigurationMetadataKey];
```
