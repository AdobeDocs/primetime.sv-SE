---
description: Referensimplementeringen för Primetime använder ett JSON-baserat feedformat för svar. Det här formatet tolkas med en implementering av IFeedItemAdapter-gränssnittet.
seo-description: Referensimplementeringen för Primetime använder ett JSON-baserat feedformat för svar. Det här formatet tolkas med en implementering av IFeedItemAdapter-gränssnittet.
seo-title: Katalogformat
title: Katalogformat
uuid: 6e1a526f-c0bb-403d-a792-666caf5479a5
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---


# Katalogformat {#catalog-format}

Referensimplementeringen för Primetime använder ett JSON-baserat feedformat för svar. Det här formatet tolkas med en implementering av IFeedItemAdapter-gränssnittet.

>[!NOTE]
>
>Detta matningsformat är det exempelformat som används och fungerar som ett exempel på hur formatet kan tolkas och mappas till matningsgränssnittet. Du kan använda ditt eget inmatningsformat med dina egna implementeringar av matningsgränssnittet.

På en hög nivå består formatet av en array med innehållsposter. Varje post representerar ett videomaterial som publiceras live eller VOD:

```
{
    "entries": [
        {
        },
        {
        },
        ...
    ]
}
```

Varje flödespost är ett JSON-objekt med en given uppsättning attribut:

```
{
    "entries": [
        
            "id": "episode1",
            "title": "My episode1",
            "description": "This is an episode.",
            "categories": "documentary, educational, children",
            "keywords": "List, of, comma, separated, keywords",
            "isLive": false,
            "content":  [
                
                },
                
                },
            ],
            "thumbnails": [
                
                },
                
                }
            ]
            "metadata": 
            } 
        }
    ]
}
```

| Egenskap | Beskrivning |
|---|---|
| `id` | En unik identifierare/guide för innehållet enligt feed-publiceringssystemet. |
| `title` | En rubrik för innehållet. |
| `description` | En beskrivning av innehållet. |
| `categories` | En lista med kategorier som taggats för innehållet och som kan användas av programmet för att förbättra användarens upplevelse. Läs mer om egenskaperna för innehållet. |
| `keywords` | En lista med kommaseparerade nyckelord kan användas av programmet för att förbättra användarens upplevelse. Läs mer om egenskaperna för innehållet. |
| `isLive` | true eller false, vilket anger om det är en Live- eller VOD-ström. |
| `content` | En array med JSON-objekt med alternativa format för innehållet tillsammans med motsvarande URL:er. Det kan till exempel finnas URL:er för formaten f4m och m3u8. JSON-objektattributen beskrivs närmare nedan. |
| `thumbnails` | En array med JSON-objekt med URL:er för olika storlekar på miniatyrbilder. JSON-objektattributen definieras nedan. |
| `metadata` | Ett JSON-objekt som definierar metadata för innehållet. För närvarande är dessa metadata begränsade till och relaterade metadata. Metadataobjektet definieras nedan. |

Följande kodblock definierar de JSON-objekt som utgör arrayen för **innehållsobjekt**:

```
"content":  [
    {
        "format": "M3U8",
        "url": "https://adobeprimetime-f.akamaihd.net/i/
<i>longstringofcharacters</i>/
                 Episode_,640x360_1000,640x360_700,_b.mp4.csmil/master.m3u8",
        "language": "en"
    }  
],
```

| Egenskap | Beskrivning |
|--- |--- |
| format | Måste vara m3u8-format för Android. |
| url | URL:en till videoströmmen för det angivna formatet. |

Följande kodblock definierar de JSON-objekt som utgör arrayen med **miniatyrbildobjekt**:

```
"thumbnails": [
    {
        "format": "JPEG",
        "height":  "90",
        "width": "160",
        "url": "https://example.com/small.jpg"
    },
    {
        "format": "JPEG",
        "height": "450",
        "width": "800",
        "url": "https://example.com/large.jpg"
    }
],
```

| Egenskap | Beskrivning |
|---|---|
| format | En sträng som anger formatet för miniatyrfilen, till exempel JPEG, PNG osv. |
| height | Höjden på miniatyrbilden. I referensprogrammet returneras miniatyrbilden med den minsta höjden och bredden som en liten miniatyrbild och den med den största bredden och höjden som en stor miniatyrbild. |
| width | Bredden på miniatyrbilden. I referensprogrammet returneras miniatyrbilden med den minsta höjden och bredden som en liten miniatyrbild och den med den största bredden och höjden som en stor miniatyrbild. |
| url | URL:en till miniatyrfilen. |

Följande kodblock definierar **metadataobjektet**:

```
"metadata" : {
    "ad" : {
        "type" : "",
        "details" : {
        }
    }
    "entitlement" : {
        "id" : ""
    }
}
```

| Egenskap | Beskrivning |
|--- |--- |
| ad | Annonsrelaterade metadata. |
| type | Värdet kan vara Primetime Ads, Direct Ad Breaks eller Custom Ad Marers. <br/><br/>PSDK har inbyggt stöd för följande typer av metadata: Auditude-relaterade metadata för Primetime Ad Serving (Primetime Ads), direkta annonsbrytningar med annonsadresser (Direct Ad Breaks) och anpassade annonsmarkörer som anger tidsintervallet för varje annonsmarkör (Custom Ad Marers). Varje typ har en inbyggd AdProvider i PSDK som bearbetar metadata.  <br/><br/>JSON-formatet för var och en av dessa har definierats nedan. |
| information | Innehåller attribut för annonsmetadata. Båda typerna av annonsmetadata har en egen uppsättning attribut som definieras nedan. För de inbyggda typerna definierar attributen de data som förväntas av PSDK för den typen. |
| berättigande | Tillståndsrelaterade metadata |
| id | Medieresurs-ID som används för auktoriseringsbegäranden mot Adobe Primetime betal-TV-pass-tjänst. ID:t kan vara antingen en textsträng eller en HTML-kodad mRSS-sträng. Allt mediainnehåll som kräver auktorisering måste innehålla ett giltigt resurs-ID. |

