---
description: Förutom de grundläggande frågeparametrarna gör valfria frågeparametrar att manifestservern kan arbeta med olika klienter och situationer.
seo-description: Förutom de grundläggande frågeparametrarna gör valfria frågeparametrar att manifestservern kan arbeta med olika klienter och situationer.
seo-title: Valfria frågeparametrar per klient och situation
title: Valfria frågeparametrar per klient och situation
uuid: e3fae41e-9f7d-4f01-9a01-52a1d5f5dad5
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Valfria frågeparametrar per klient och situation {#optional-query-parameters-by-client-and-situation}

Förutom de grundläggande frågeparametrarna gör valfria frågeparametrar att manifestservern kan arbeta med olika klienter och situationer.

## Lägga till annonser med Akamai Ad Scaler {#section_120FEC75C34D4F4587B77D842166D68A}

På Akamai Content Delivery Network (CDN) fungerar Akamai Edge-servern som en mellanhand mellan klienten och manifestservern. Om du även använder Ad Scaler innehåller parametrarna `ptassetid` och `live` query den information som krävs till Akamai Edge.

Parametern `ptassetid` är utgivarens ID för dess mediefil. Akamai använder detta, i stället för den base64-kodade URL-adressen som du anger som en del av förfrågnings-URL:en, för att identifiera den spellista som ska tillhandahållas manifestservern för annonsinfogning.

Parametern `live` skiljer mellan live-innehåll och on demand-video (VOD). Manifestservern behöver den här informationen för att stödja det smidiga gränssnittet med Akamai.

Här följer ett exempel-URL som visar parametrarna som gäller för Akamai:

```
https://. . .master.m3u8?. . .&ptassetid=pubAsset&live=true
```

## Annonsinfogning från TVSDK på Xbox {#section_5DB405F4647240A0B83E72DE35D5EC80}

En spelare som är baserad på Primetime TVSDK på Xbox behöver inte tillhandahålla ytterligare frågeparametrar utöver de grundläggande.

## Lägga till annonser från TVSDK på iOS med Safari {#section_250E493A125E4F82940D19C7DA2AAB2E}

En spelare som baseras på Primetime TVSDK på iOS med webbläsaren Safari måste ange parametrarna `ptplayer` och `live` förutom de grundläggande frågeparametrarna.

Manifestservern känner igen `ptplayer` värdet `ios-mobileweb` och tar bort förrullningen från det annonssammansatta manifest som returneras.

Parametern anger `live` om manifestservern ska returnera live- eller VOD-innehåll.

Här följer ett exempel-URL som visar parametrarna som gäller iOS med Safari:

```
https://. . .master.m3u8?. . .&ptplayer=ios-mobileweb&live=false
```

## Lägga till annonser med ett anpassat annonsformat {#section_82AF880AAABE4BD4B593D906434D4D89}

Adobe tillhandahåller namn på annonsformat som inte stöds direkt i Primetime-paketet. Om du vill använda ett sådant format anger du det Adobe-angivna namnet som värdet på `ptcueformat` parametern.

Här följer ett exempel-URL som anger ett anpassat annonsformat:

```
https://. . .master.m3u8?. . .&ptcueformat=[custom format name]
```

## Annonsinfogning med hjälp av annonsinfogningar för att skapa en FreeWheel-tidslinje för VOD {#section_E0D830F5EEE24639819B975B90F6999F}

För VOD-innehåll som innehåller annonser som ska tolkas och inkluderas i en FreeWheel-annonsbegäran anger du värdet för `ptcueformat` parametern till `DPIsimple`.

Här är ett exempel-URL som anger hur en FreeWheel-tidslinje används för VOD:

```
https://. . .master.m3u8?. . .&ptcueformat=DPISimple&live=false
```

## Annonsinfogning med en anpassad tidslinje för VOD {#section_F398F7659164463FA886A4CC787C7B5A}

Om du vill be manifestservern att infoga annonser i VOD-innehåll enligt en tidslinje som du anger, anger du värdet för `pttimeline` parametern till en sträng som anger tidslinjen. Se [VOD-tidslinjeformat](../../msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)

Här följer ett exempel-URL som använder en anpassad tidslinje för VOD:

```
https://. . .master.m3u8?. . .&live=false&pttimeline=B,60,2,p;C,120,1;B,30,2,m;C,300,1
```

Det specificerar en inledande brytning på en minut som innehåller upp till två annonser, följt av ett innehållssegment på två minuter, följt av en brytning på 30 sekunder som innehåller upp till två annonser, följt av ett innehållssegment på fem minuter.

Lägga till sammanfogning för en anpassad innehållstidslinje för VOD-innehåll fungerar på följande sätt:

* Annonsen visas i den närmaste brytningsgränsen efter den annonsplaceringstid som anges av annonsservern.
* Segmenten är minst två sekunder långa.

## Auktorisera TS-segment {#section_BF855A4399DC42CB8C0586113A416BBC}

Adobe stöder endast den här funktionen för Akamai CDN. HTTP-direktuppspelning (HLS) levererar TS-segment (Transport Stream) med hjälp av en M3U8-spellista på direktuppspelningsnivå. Flera spellistor på direktuppspelningsnivå tillhandahålls klienten i en variant av M3U8-spellista. Klienten väljer en spellistström från variantlistan och hämtar sedan TS-segment i den strömnivåspellistan en i taget. Vid normal användning kan det begärda innehållet kräva auktorisering av cookies, som manifestservern hanterar osynligt i bakgrunden. Den extraherar cookien från det råa innehållet och lägger till en lämplig token till den URL som ska användas för att begära den valda spellistströmmen.

När frågeparametrarna för Bootstrap-URL:en innehåller `pttoken=true`kräver utgivaren en cookie som ska användas för att begära varje TS-segment, i stället för bara en gång för hela flödet. Manifestservern kopplar denna cookie som en frågeparameter till varje TS-segment-URL i den flödesspellista som skickas tillbaka.
