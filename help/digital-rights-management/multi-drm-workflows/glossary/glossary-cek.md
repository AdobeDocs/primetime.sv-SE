---
title: Ordlista
description: Vanliga termer som kräver en särskild definition.
exl-id: 4e7874f7-c5c0-4f2c-ada2-a0da3ed4d4bf
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Ordlista {#glossary}

Vanliga termer som kräver en särskild definition.

## Innehållskrypteringsnyckel {#content-encryption-key}

Innehållskrypteringsnyckeln (CEK), som genereras av ett verktyg, används därefter av en innehållspaketerare vid förberedelse av innehåll som måste skyddas.
Verktyget genererar nyckeln i hex med en längd på 16 byte.
I den här guiden visas följande varianter av parameternamn och värdenamn för CEK i anteckningar och felmeddelanden, filer och kommandoexempel:

* innehållsnyckel
* `&contentKey=`
* `?cek=`
* `<CEK>`
* `[YOUR CONTENT KEY]`

Filnamn för en CEK visas som:

* `keyfile.bin`
* `creds/fairplaybin`
* `Jaigo_DASH/_info/key.B64.random`

CEK:n kan lagras i ett nyckelhanteringssystem samt krypteras. Den här guiden refererar till lagringsindexet CEK Storage ID CEKSID. Termen Nyckelkrypteringsnyckel (KEK) avser krypteringsnyckeln på andra nivån och termen `ek` refererar till värdet för den krypteringen.
Vissa samtal använder både CEK och CEK Storage ID CEKSID, och CEK som hämtas från lagring måste matcha CEK som tillhandahålls i samtalet.
För HLS Offline med FairPlay finns det även en `persistentContentKey` som kan förfalla.

## Lagrings-ID för innehållskrypteringsnyckel {#content-encryption-key-storage-id}

CSID (Content Encryption Key Storage ID) är ett ID som används för att hämta en innehållskrypteringsnyckel från ett nyckelhanteringssystem.

CEKSID kallas också
* Nyckel-ID
* Innehålls-ID
* `&kid`

## Kundautentisering {#customer-authenticator}

En nyckel för autentisering i begäranden till API:t för uttryck. Förfrågningar kan innehålla förfrågningar om tokens.
