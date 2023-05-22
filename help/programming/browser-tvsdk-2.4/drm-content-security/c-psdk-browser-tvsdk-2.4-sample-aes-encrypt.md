---
description: Krypteringsmetoden AES-128 krypterar hela TS-behållaren (Transport Stream) inklusive rubriker, men krypteringen i SAMPLE-AES krypterar bara ljudet och en del av videodata.
title: Exempel på AES-krypterade HLS-strömmar
exl-id: 04bda50f-5ca4-4a00-bb5a-97259a2cb005
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Exempel på AES-krypterade HLS-strömmar{#sample-aes-encrypted-hls-streams}

Krypteringsmetoden AES-128 krypterar hela TS-behållaren (Transport Stream) inklusive rubriker, men krypteringen i SAMPLE-AES krypterar bara ljudet och en del av videodata.

I krypterade strömmar identifieras ett skyddat block över vilket skyddsprocessen slutförs. H.264-videoskyddade block är brödtexten för typerna 1 och 5 i NAL-enheter (Network Customization Layer). Ett skyddat ljudblock är en ljudbildruta och ljudet måste vara i AAC-format.

>[!IMPORTANT]
>
>Du måste ha nyckeln och initieringsvektorn (IV). I webbläsaren TVSDK används nyckeln och IV för att dekryptera strömmen innan den spelas upp.

Varje skyddat block innehåller ett heltal på 16-byte-block som krypteras i CBC-läget (AES-128 cipher block-chaining) utan utfyllnad. CBC förekommer i varje skyddat block och i början av varje nytt skyddat block måste IV återställas till sitt ursprungliga värde.

Följande kodekar stöds:

* För video stöds H.264.
* För ljud stöds sample-AES bara för AAC.
