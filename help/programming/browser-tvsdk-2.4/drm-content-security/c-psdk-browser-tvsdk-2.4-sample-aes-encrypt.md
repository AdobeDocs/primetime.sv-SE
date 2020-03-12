---
description: Krypteringsmetoden AES-128 krypterar hela TS-behållaren (Transport Stream) inklusive rubriker, men krypteringen i SAMPLE-AES krypterar bara ljudet och en del av videodata.
seo-description: Krypteringsmetoden AES-128 krypterar hela TS-behållaren (Transport Stream) inklusive rubriker, men krypteringen i SAMPLE-AES krypterar bara ljudet och en del av videodata.
seo-title: Exempel på AES-krypterade HLS-strömmar
title: Exempel på AES-krypterade HLS-strömmar
uuid: 32c1f87b-eb81-4e1c-92ea-ec37260a7ecb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

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

