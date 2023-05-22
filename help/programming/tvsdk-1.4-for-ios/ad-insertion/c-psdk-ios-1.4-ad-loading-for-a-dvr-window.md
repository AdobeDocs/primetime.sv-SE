---
description: Du kan bestämma om du bara vill matcha annonser som inträffar efter användarens aktuella Live Point eller om du även vill matcha annonser som inträffar före den aktuella Live-punkten.
title: Läs in annons för ett DVR-fönster
exl-id: f0799002-5cba-41c2-86bb-9ccf6b906357
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Läs in annons för ett DVR-fönster {#load-ad-for-a-dvr-window}

Du kan bestämma om du bara vill matcha annonser som inträffar efter användarens aktuella Live Point eller om du även vill matcha annonser som inträffar före den aktuella Live-punkten.

När en användare börjar visa innehåll i början av en DVR-ström, löser TVSDK alla annonser för strömmen vid den tidpunkten. Men när användaren börjar visa innehåll vid en punkt efter direktuppspelningens början kan du bestämma om endast de annonser som visas efter användarens aktuella direktpunkt ska matchas eller om annonser som har gjorts före den aktuella direktpunkten ska matchas.

>[!TIP]
>
>Reparera annonser efter att den aktuella direktpunkten är snabbare, men om användaren söker bakåt förhindrar det här alternativet spelaren från att spela upp annonser som visades tidigare.

## Styra och läsa in för ett DVR-fönster {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Så här styr du inläsning av DVR-fönster:

Om du vill läsa in alla annonser för hela flödet anger du `PTAdMetadata.enableDVRAds` egenskap till `YES`.

>[!NOTE]
>
>Standardvärdet är `NO`och det här alternativet läser bara in annonser från den aktuella direktpunkten.

Till exempel:

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
 
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
adMetadata.zoneId = <ZoneId>; 
adMetadata.domain = <Domain>; 
 
// Enable DVR Ads by setting to YES the enableDVRAds property on PTAdMetadata  
// (PTAuditudeMetadata is a subclass of PTAdMetadata)  
adMetadata.enableDVRAds = YES; 
 
[metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
 
//Create PTMediaPlayerItem with the previously prepared metadata    
playerItem = [[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata]; 
```
