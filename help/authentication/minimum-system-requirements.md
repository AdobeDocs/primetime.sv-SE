---
title: Lägsta systemkrav
description: Lägsta systemkrav
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# Lägsta systemkrav {#minimum-system-requirements}

>[!NOTE]
>
>Innehållet på den här sidan tillhandahålls endast i informationssyfte. Användning av denna API kräver en aktuell licens från Adobe. Ingen obehörig användning är tillåten.


## Översikt {#overview}

Det här dokumentet innehåller aktuella program- och maskinvarukrav för implementering av Adobe Primetime Authentication-integreringar på plattformar som stöds. Alla webbläsare och operativsystem som stöds på webben/mobilen och som listas nedan har fullt stöd för Adobe Primetime Authentication Team, som är bundna till de överenskomna SLA:erna.

Vi som Adobe Primetime Authentication-team rekommenderar att man använder de senaste stabila versionerna av webbläsarna och operativsystemen. Vi är också medvetna om att det finns inkompatibla/äldre plattformar och webbläsare som används. Dessa inaktuella enheter kan fortfarande fungera utan problem, men de har större felbenägenhet.

Inledande åtgärder för att minska eventuella problem som uppstår på dessa gamla plattformar bör vara att uppgradera till de senaste versionerna. Det kan vara operativsystemets version, webbläsarversionen eller versionen av det installerade programmet.

Problem som uppstår på dessa plattformar hanteras som en bas för bästa insatser av Adobe Primetime autentiseringsteam. 

Adobe Primetime uppmuntrar våra kunder och partners att överväga att uppgradera till de senaste versionerna för att dra nytta av Adobe fullständiga support i eventuella problem, utöver prestandaförbättringar, effektivitetsförbättringar och säkerhetsförbättringar. 


## Krav för webbläsare och operativsystem {#browser-OS-system-requirements}


| Webb-/mobilwebbläsare (†) | Versioner som stöds |
|---|---|
| Google Chrome | **70** eller senare |
| Mozilla Firefox | **57** eller senare |
| Apple Safari | **14** eller senare |
| Microsoft Edge | **100** eller senare |

(†) Adobe avråder från att använda privat läge eller inkognito-läge.

| Operativsystem | Versioner som stöds |
|---|---|
| *Android* | **7.0** (Nougat) eller senare |
| *iOS* | **14** eller senare |
| *iPadOS* | **14** eller senare |
| *tvOS* | **14** eller senare |
| *Fire OS* | **5 (Android 5.1)** eller senare |
| *Mac OS* | **10.13** eller senare |
| *Microsoft Windows* | **10** eller senare |




>[!NOTE]
>
>Cookies från tredje part - Rättighetsflöden för Adobe Primetime-autentisering kan misslyckas när cookies från tredje part inaktiveras.  Problemet uppstår bara när webbläsarinställningarna ändras. För alla webbläsare som stöds bör Primetime-autentisering fungera med standardinställningarna.\
 

## Enhetskrav för implementeringar av klientlösa (REST) {#general_clientless_reqs}

 
Alla enheter som använder Adobe Primetime autentiseringstjänster via klientlösa implementeringar **måste kunna**:

* Ange ett unikt, hash-kodat enhets-ID. Om enheten inte har ett unikt hash-kodat enhets-ID måste den kunna behålla ett unikt ID som tillhandahålls av Adobe Primetime Authentication. Enheten bör kunna behålla det unika ID:t permanent i sin lokala lagring och tillhandahålla det unika ID:t som enhets-ID när den anropar Adobe Primetime Authentication API:er.
* Generera digitala signaturer med HMAC-SHA1-algoritmen
* Ange godtyckliga HTTP-rubriker
* Förbruka RESTful-webbtjänster
* Tolka XML- och JSON-dataformat
* Skicka trafik med HTTPS
* Hantera HTTP-felkoder
