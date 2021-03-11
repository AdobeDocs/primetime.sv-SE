---
title: Översikt över verktyget AIR Publisher ID
description: Översikt över verktyget AIR Publisher ID
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Översikt över verktyget AIR Publisher ID {#air-publisher-id-utility-overview}

Som en del av processen att skapa en AIR-fil genererar AIR Developer Tool (ADT) ett utgivar-ID. Detta är en identifierare som är unik för det certifikat som används för att skapa AIR-filen. Om du återanvänder samma certifikat för flera AIR-program har de samma utgivar-ID. Verktyget AIR Publisher ID används för att beräkna utgivar-ID:t för ett AIR-program. AIR-versioner efter 1.5.2 skriver inte det genererade utgivar-ID:t till en fil, så det är nödvändigt att använda det här verktyget för att fastställa utgivar-ID:t om du använder ett AIR-program tillåtelselista.

>[!NOTE]
>
>Utgivar-ID:t, som används för att använda AIR tillåtelselista, är inte detsamma som det utgivar-ID som anges av programutgivaren i programmets [!DNL application.xml]-fil.
