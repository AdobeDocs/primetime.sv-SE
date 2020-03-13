---
description: Multi CDN gör det möjligt att ställa in en eller flera CDN-platser för transkodade annonser.
seo-description: Multi CDN gör det möjligt att ställa in en eller flera CDN-platser för transkodade annonser.
seo-title: Stöd för flera CDN
title: Stöd för flera CDN
uuid: 2b6d71f0-61c8-486b-a35a-f7ef3a9519d2
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff

---


# Stöd för flera CDN {#multi-cdn-support}

Multi CDN gör det möjligt att ställa in en eller flera CDN-platser för transkodade annonser.

Som standard lagras alla omkodade resurser på det Adobe-ägda Akamai CDN. Du kan dock välja noll eller flera ytterligare CDN-platser på din egen plats där CRS är värd för den omkodade resursen. I det här fallet kan dina omkodade resurser och innehåll hanteras från samma CDN.

När manifestservern gör en sökning efter omkodade begäranden, används en bootstrap-URL som innehåller ett antal frågeparametrar. Om du har konfigurerat en miljö med flera CDN-anslutningar måste bootstrap-URL:en även innehålla `ptcdn` parametern. Manifestservern använder den här parametern för att identifiera CDN-servern som annonsens omkodade version ska hämtas från.

Multi CDN-stöd finns även för följande Primetime-lösningar:

1. TVSDK för Android
1. TVSDK for Desktop HLS
1. TVSDK för iOS

## Aktivera CDN-stöd {#section_1BA344F2300B49F291865A7461EDFEAE}

CRS är som standard inaktiverat för alla kunder

Kontakta din tekniska kontohanterare på Adobe för att konfigurera ditt CRS-konto så att andra CDN:er kan användas som värd för de omkodade annonsresurserna. Du måste ange följande information som CRS behöver för att kunna överföra de omkodade annonsresurserna till CDN

1. CDN-URL
1. Autentiseringsinformation
1. Utdata-URL-format

Din kontoansvarige på Adobe ger dig också ett smeknamn för det här CDN:et. Du måste skicka det som värdet för `ptcdn` parametern i Bootstrap-URL:en.

Du kan konfigurera flera CDN:er i CRS end via Adobes support. Det CDN som används för att plocka annonsresurser som ska sammanfogas via manifestservern måste dock vara det som skickas som värde för `ptcdn` parametern i Bootstrap-URL:en.
