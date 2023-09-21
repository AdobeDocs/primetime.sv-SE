---
title: Vanligt arbetsflöde
description: Vanligt arbetsflöde
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
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
