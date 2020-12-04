---
description: Du kan bestämma om du bara vill matcha annonser som inträffar efter användarens aktuella Live Point eller om du även vill matcha annonser som inträffar före den aktuella Live-punkten.
seo-description: Du kan bestämma om du bara vill matcha annonser som inträffar efter användarens aktuella Live Point eller om du även vill matcha annonser som inträffar före den aktuella Live-punkten.
seo-title: Läs in annons för ett DVR-fönster
title: Läs in annons för ett DVR-fönster
uuid: 3ae1fbf6-deae-4f39-a17d-43d1fe3cb975
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# Läs in annons för ett DVR-fönster {#load-ad-for-a-dvr-window}

Du kan bestämma om du bara vill matcha annonser som inträffar efter användarens aktuella Live Point eller om du även vill matcha annonser som inträffar före den aktuella Live-punkten.

När en användare börjar visa innehåll i början av en DVR-ström, löser TVSDK alla annonser för strömmen vid den tidpunkten. Men när användaren börjar visa innehåll vid en punkt efter direktuppspelningens början kan du bestämma om endast de annonser som visas efter användarens aktuella direktpunkt ska matchas eller om annonser som har gjorts före den aktuella direktpunkten ska matchas.

>[!TIP]
>
>Reparera annonser efter att den aktuella direktpunkten är snabbare, men om användaren söker bakåt förhindrar det här alternativet spelaren från att spela upp annonser som visades tidigare.

## Kontrollera och läsa in ett DVR-fönster {#section_2D93E2E947644D66B6F6ED1DD6742C25}

Så här styr du inläsning av DVR-fönster:

    Om du vill läsa in alla annonser för hela flödet anger du egenskapen &quot;PTAdMetadata.enableDVRAds&quot; till &quot;YES&quot;.

>[!NOTE]
>
>Standardvärdet är `NO`, och det här alternativet läser bara in annonser från den aktuella direktpunkten.

Exempel:

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
