---
description: Multi CDN gör det möjligt att ställa in en eller flera CDN-platser för transkodade annonser.
seo-description: Multi CDN gör det möjligt att ställa in en eller flera CDN-platser för transkodade annonser.
seo-title: Stöd för flera CDN
title: Stöd för flera CDN
uuid: 2b6d71f0-61c8-486b-a35a-f7ef3a9519d2
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Multi CDN-stöd {#multi-cdn-support}

Multi CDN gör det möjligt att ställa in en eller flera CDN-platser för transkodade annonser.

Som standard lagras alla omkodade resurser på det Adobe-ägda Akamai CDN. Du kan dock välja noll eller flera ytterligare CDN-platser på din egen plats där CRS är värd för den omkodade resursen. I det här fallet kan dina omkodade resurser och innehåll hanteras från samma CDN.

När manifestservern gör en sökning efter omkodade begäranden, används en bootstrap-URL som innehåller ett antal frågeparametrar. Om du har konfigurerat en miljö med flera CDN-anslutningar måste bootstrap-URL:en också innehålla parametern `ptcdn`. Manifestservern använder den här parametern för att identifiera CDN-servern som den omkodade versionen av annonsen ska hämtas från.

Multi CDN-stöd finns även för följande Primetime-lösningar:

1. TVSDK för Android
1. TVSDK for Desktop HLS
1. TVSDK för iOS

## Aktivera CDN-stöd {#section_1BA344F2300B49F291865A7461EDFEAE}

CRS är som standard inaktiverat för alla kunder

Kontakta den tekniska kontohanteraren för Adobe för att konfigurera ditt CRS-konto så att andra CDN:er kan användas som värd för omkodade annonsresurser. Du måste ange följande information som CRS behöver för att kunna överföra omkodade annonsresurser till CDN

1. CDN-URL
1. Autentiseringsinformation
1. Utdata-URL-format

Din kontoansvarige på Adobe kommer också att ge dig ett smeknamn för det här CDN-numret. Du måste skicka det som värdet för parametern `ptcdn` i Bootstrap-URL:en.

Du kan konfigurera flera CDN:er i CRS end via stöd för Adobe. Det CDN som används för att plocka annonsresurser som ska sammanfogas via manifestservern måste dock vara det som skickas som värde för parametern `ptcdn` i URL:en för Bootstrap.
