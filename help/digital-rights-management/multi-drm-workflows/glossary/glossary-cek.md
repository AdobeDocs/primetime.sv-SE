---
uuid: 2d927ae8-4c4b-4b64-88b8-9c86430e226c
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '225'
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

CEK:n kan lagras i ett nyckelhanteringssystem samt krypteras. Den här guiden refererar till lagringsindexet CEK Storage ID CEKSID. Termen Nyckelkrypteringsnyckel (KEK) refererar till krypteringsnyckeln på den andra nivån och termen `ek` refererar till krypteringsvärdet.
Vissa samtal använder både CEK och CEK Storage ID CEKSID, och CEK som hämtas från lagring måste matcha CEK som tillhandahålls i samtalet.
För HLS Offline med FairPlay finns också ett `persistentContentKey`-värde som kan förfalla.

## Lagring-ID för innehållskrypteringsnyckel {#content-encryption-key-storage-id}

CSID (Content Encryption Key Storage ID) är ett ID som används för att hämta en innehållskrypteringsnyckel från ett nyckelhanteringssystem.

CEKSID kallas också
* Nyckel-ID
* Innehålls-ID
* `&kid`

## Kundens autentisering {#customer-authenticator}

En nyckel för autentisering i begäranden till API:t för uttryck. Förfrågningar kan innehålla förfrågningar om tokens.