---
seo-title: Översikt över verktyget AIR Publisher ID
title: Översikt över verktyget AIR Publisher ID
uuid: 31aecc0e-ad9b-43ad-ba58-77d2c999f4a4
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Översikt över verktyget AIR Publisher ID {#air-publisher-id-utility-overview}

Som en del av processen att skapa en AIR-fil genererar AIR Developer Tool (ADT) ett utgivar-ID. Detta är en identifierare som är unik för det certifikat som används för att skapa AIR-filen. Om du återanvänder samma certifikat för flera AIR-program har de samma utgivar-ID. Verktyget AIR Publisher ID används för att beräkna utgivar-ID:t för ett AIR-program. AIR-versioner efter 1.5.2 skriver inte det genererade utgivar-ID:t till en fil, så det är nödvändigt att använda det här verktyget för att fastställa utgivar-ID:t om du använder ett AIR-program tillåtelselista.

>[!NOTE]
>
>Utgivar-ID:t, som används för att använda AIR tillåtelselista, är inte detsamma som det utgivar-ID som anges av programutgivaren i programmets [!DNL application.xml] fil.
