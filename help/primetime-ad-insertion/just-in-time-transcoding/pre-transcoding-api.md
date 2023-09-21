---
title: API för förkodning
description: Du kan använda API:t för just-in-time-ompaketering för att koda annonsprojekt i förväg, så att det finns en innehållskompatibel version tillgänglig när det behövs, vilket eliminerar den 2-4 minuters fördröjning som är kopplad till just-in-time-ompaketering (JIT).
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# API för förtranskodning och ompaketering {#pre-transcoding-api}

Primetime Ad Insertion erbjuder ett förtranskodnings-API för situationer där kreativa URL:er är kända i förväg, till exempel för stora direktsålda händelser.  Detta eliminerar 2-4 minuters fördröjning i samband med just-in-time-omkodning.

## HTTP-begäran {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

Skicka ett HTTP-POST-kommando till den angivna URL:en för att tala om för CRS vilken annons du vill omkoda och vilka alternativ du vill att den ska använda. Svarskoden rapporterar om det går eller inte och annan information.

Denna begäran kräver ett användarnamn och lösenord. Du kan få dessa från din kontoansvarige på Adobe. Om du vill ha information om autentiseringen kontaktar du Adobe Primetime Enablement.

Om du vill skicka en begäran om omkodning till CRS skickar du ett HTTP-meddelande enligt följande:

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **Metod -** `POST`

* **Autentisering -** `Digest`

* **Rubrik -** `Content-Type: text/xml`

* **Brödtext -** XML som i följande exempel:

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

The `RepackageList` -block i brödtexten kan innehålla 1 till 300 `Repackage` -block. Om antalet `Repackage` -block i brödtexten överstiger 300, då misslyckas HTTP-begäran med följande fel:

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


obligatoriska och valfria parametrar i en `Repackage` -block är som följer:

* **`AdSystem`** (Obligatoriskt) - Källservern, till exempel `Auditude`, `FreeWheel`, `Apad.tv`. Detta är ett strängvärde som motsvarar VAST-elementet `AdSystem`.

* **`AdId`** (Obligatoriskt) - Detta är en identifierare för den tredjepartsserver som anges i begäran. Den motsvarar `id` attributet för `Ad` i ett VAST-svar.

* **`CreativeURL`** (Obligatoriskt) - Platsen (URI) för annonsen som ska omkodas. Detta motsvarar VAST. `MediaFile` -element.

* `CreativeID` (valfritt) - Identifieraren för annonsen som ska inkluderas som en del av annonsupplevelsen.
* **`Zone`** (Obligatoriskt) - Zon-ID för ditt konto (hämtas från din tekniska kontohanterare). Detta är ett numeriskt värde som motsvarar plattformen Auditude `publisher_site_id` inställning.

* **`Format`** (valfritt) - Parametrar för att styra hur CRS omkodar annonsens kreativitet:

   * `clientside` - Generera utdata som är kompatibla med den URL som TVSDK använder för att kommunicera med CDN.

  >[!IMPORTANT]
  >
  >Du måste ange den här parametern om du vill att den ompaketerade annonsen ska vara kompatibel med Ad Insertion på klientsidan. Om du inte anger detta kommer den ompaketerade annonsen endast att vara kompatibel med Ad Insertion på serversidan.

   * `hls` - Generera en HLS-kompatibel trancoded creative.
   * `dash` - Generera en DASH-kompatibel trancoded creative.
   * `id3` - Lägg in ID3-taggar med tidsmetadata i den omkodade annonsen.
   * `targetdur` - Segmentets varaktighet (i sekunder) för den omkodade annonsen. Standard är `targetdur=4`. Detta värde ska motsvara värdet som anges i manifestet för `<s>` i målvaraktighetstaggen: `#EXT-X-TARGETDURATION:<s>`.

  >[!NOTE]
  >
  >DASH-kompatibla resurser är inte kompatibla med infogning av Adobe Primetime-annonser.

>[!IMPORTANT]
>
>För att uppspelningen ska bli så smidig som möjligt anger du `targetdur` för att matcha innehållets segmentvaraktighet.

## HTTP-svar {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS svarar på begäran med någon av följande statuskoder:

* **HTTP 202** - Accepterad (med tom brödtext). Detta visar att det lyckades. CRS överför den omkodade annonsen till CDN-servern.
* **HTTP 400** - Felaktig begäran. Den bokförda XML-filen är ogiltig.
* **HTTP 500** - Internt serverfel. Servern påträffade ett internt problem (servern kunde till exempel inte ansluta till en databas).

## Förkoda resurser för SSAI eller CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}

Med API:t för ompaketering kan du förkoda framtida SSAI- eller CSAI-händelser. Om tillgångarna är avsedda att användas med SSAI i framtiden, måste du se till att alla parametrar i POSTEN är unika. Parametrarna är: AdSystem, AdId, CreativeURL, Zone, Format. Eventuella skillnader i den här parameteruppsättningen resulterar i en ny omkodningsbegäran för SSAI.

För resurser som används med CSAI i framtiden beror resursens unika karaktär på Zone och CreativeURL. AdSystem och AdId resulterar inte i olika omkodade resurser och dessa är tillgängliga för klienter.
