---
description: Multi CDN gör det möjligt att ställa in en eller flera CDN-platser för transkodade annonser.
title: Stöd för flera CDN
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# Stöd för flera CDN {#multi-cdn-support}

Multi CDN gör det möjligt att ställa in en eller flera CDN-platser för transkodade annonser.

Som standard lagras alla omkodade resurser på det Adobe-ägda Akamai CDN. Du kan dock välja noll eller flera ytterligare CDN-platser på din egen plats där CRS är värd för den omkodade resursen. I det här fallet kan dina omkodade resurser och innehåll hanteras från samma CDN.

När manifestservern gör en sökning efter omkodade begäranden, används en bootstrap-URL som innehåller ett antal frågeparametrar. Om du har konfigurerat en multi-CDN-miljö måste bootstrap-URL:en även innehålla `ptcdn` parameter.Manifestservern använder den här parametern för att identifiera CDN-servern som annonsens omkodade version ska hämtas från.

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

Din kontoansvarige på Adobe kommer också att ge dig ett smeknamn för det här CDN-numret. Du måste skicka det som värdet för `ptcdn` i Bootstrap URL.

Du kan konfigurera flera CDN:er i CRS end via stöd för Adobe. Det CDN som används för att plocka annonsresurser som ska sammanfogas via manifestservern måste dock vara det som skickas som värdet för `ptcdn` i Bootstrap URL.
