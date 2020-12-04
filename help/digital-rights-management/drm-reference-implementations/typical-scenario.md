---
description: 'null'
seo-description: 'null'
seo-title: Vanligt arbetsflöde
title: Vanligt arbetsflöde
uuid: aafe0030-8a59-4090-aeac-76867777eaa5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Vanligt arbetsflöde{#typical-workflow}

Detta är ett typiskt arbetsflöde för implementering av DRM-referenser i Primetime som innehåller både kommandoradsverktygen och licensservern:

1. Skapa en DRM-princip med kommandoradsverktyget Policy.
1. Kryptera innehåll med kommandoradsverktyget i Packager.
1. Distribuera referensimplementeringslicensservern.
1. Överför en videospelare till en webbserver.
1. Använd den överförda videospelaren för att hämta en licens och spela upp ditt krypterade innehåll.

Eftersom både kommandoradsverktygen och licensservern används i det här arbetsflödet bör du installera och konfigurera båda komponenterna innan du fortsätter.
