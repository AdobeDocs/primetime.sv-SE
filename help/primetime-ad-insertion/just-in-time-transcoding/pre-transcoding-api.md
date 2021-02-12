---
title: API för förkodning
description: Du kan använda API:t för just-in-time-ompaketering för att koda annonsprojekt i förväg, så att det finns en innehållskompatibel version tillgänglig när det behövs, vilket eliminerar den 2-4 minuters fördröjning som är kopplad till just-in-time-ompaketering (JIT).
seo-description: Du kan använda API:t för just-in-time-ompaketering för att koda annonsprojekt i förväg, så att det finns en innehållskompatibel version tillgänglig när det behövs, vilket eliminerar den 2-4 minuters fördröjning som är kopplad till just-in-time-ompaketering (JIT).
seo-title: API för förkodning
uuid: 03cd2428-510a-4b99-8496-059a48d5abba
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# Förkoda och ompaketera API {#pre-transcoding-api}

Primetime Ad Insertion erbjuder ett förtranskodnings-API för situationer där kreativa URL:er är kända i förväg, till exempel för stora direktsålda händelser.  Detta eliminerar 2-4 minuters fördröjning i samband med just-in-time-omkodning.

## HTTP-begäran {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Skicka ett HTTP-POST-kommando till den angivna URL:en för att tala om för CRS vilken annons du vill omkoda och vilka alternativ du vill att den ska använda. Svarskoden rapporterar om det går eller inte och annan information.

Denna begäran kräver ett användarnamn och lösenord. Du kan få dessa från din kontoansvarige på Adobe. Kontakta din Adobe Primetime-representant om du behöver information om hur du autentiserar.

Om du vill skicka en begäran om omkodning till CRS skickar du ett HTTP-meddelande enligt följande:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Metod -** `POST`

* **Autentisering -** `Digest`

* **Rubrik -** `Content-Type: text/xml`

* **Body -** XML som i följande exempel:

   ```xml
   <RepackageList>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD1</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Zone>3</Zone>
       </Repackage>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD2</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Format>id3 targetdur=5</Format>
           <Zone>3</Zone>
       </Repackage>
   </RepackageList>
   ```

`RepackageList`-blocket i brödtexten kan innehålla 1 till 300 `Repackage`-block. Om antalet `Repackage`-block i brödtexten överstiger 300 kommer HTTP-begäran att misslyckas med följande fel:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


De obligatoriska och valfria parametrarna i ett `Repackage`-block är följande:

* **`AdSystem`** (Obligatoriskt) - Källannonsservern, till exempel  `Auditude`,  `FreeWheel`,  `Apad.tv`. Detta är ett strängvärde som motsvarar VAST-elementet `AdSystem`.

* **`AdId`** (Obligatoriskt) - Detta är en identifierare för den tredjepartsserver som anges i begäran. Det motsvarar attributet `id` för `Ad`-elementet i ett VAST-svar.

* **`CreativeURL`** (Obligatoriskt) - Platsen (URI) för annonsen som ska omkodas. Detta motsvarar VAST-elementet `MediaFile`.

* `CreativeID` (valfritt) - Identifieraren för annonsen som ska inkluderas som en del av annonsupplevelsen.
* **`Zone`** (Obligatoriskt) - Zon-ID för ditt konto (hämtas från din tekniska kontohanterare). Detta är ett numeriskt värde som motsvarar Auditude-plattformen `publisher_site_id`-inställningen.

* **`Format`** (valfritt) - Parametrar för att styra hur CRS omkodar annonsens kreativitet:

   * `clientside` - Generera utdata som är kompatibla med den URL som TVSDK använder för att kommunicera med CDN.
   >[!IMPORTANT]
   >
   >Du måste ange den här parametern om du vill att den ompaketerade annonsen ska vara kompatibel med Ad Insertion på klientsidan. Om du inte anger detta kommer den ompaketerade annonsen endast att vara kompatibel med Ad Insertion på serversidan.

   * `hls` - Generera en HLS-kompatibel trancoded creative.
   * `dash` - Generera en DASH-kompatibel trancoded creative.
   * `id3` - Lägg in ID3-taggar med tidsmetadata i den omkodade annonsen.
   * `targetdur` - Segmentets varaktighet (i sekunder) för den omkodade annonsen. Standardvärdet är `targetdur=4`. Det här värdet ska motsvara det värde som anges i manifestet för `<s>` i taggen för målvaraktighet: `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >DASH-kompatibla resurser är inte kompatibla med infogning av Adobe Primetime-annonser.

>[!IMPORTANT]
>
>För att uppspelningen ska bli så jämn som möjligt ställer du in `targetdur` så att den matchar innehållets segmentlängd.

## HTTP-svar {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS svarar på begäran med någon av följande statuskoder:

* **HTTP 202**  - Accepterad (med tom brödtext). Detta visar att det lyckades. CRS överför den omkodade annonsen till CDN-servern.
* **HTTP 400**  - Felaktig begäran. Den bokförda XML-filen är ogiltig.
* **HTTP 500**  - Internt serverfel. Servern påträffade ett internt problem (servern kunde till exempel inte ansluta till en databas).

## Förkoda resurser för SSAI eller CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Med API:t för ompaketering kan du förkoda framtida SSAI- eller CSAI-händelser. Om tillgångarna är avsedda att användas med SSAI i framtiden, måste du se till att alla parametrar i POSTEN är unika. Parametrarna är: AdSystem, AdId, CreativeURL, Zone, Format. Eventuella skillnader i den här parameteruppsättningen resulterar i en ny omkodningsbegäran för SSAI.

För resurser som används med CSAI i framtiden beror resursens unika karaktär på Zone och CreativeURL. AdSystem och AdId resulterar inte i olika omkodade resurser och dessa är tillgängliga för klienter.
