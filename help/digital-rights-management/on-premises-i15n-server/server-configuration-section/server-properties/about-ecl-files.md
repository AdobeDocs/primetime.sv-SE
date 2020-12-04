---
seo-title: Om ECI-filer
title: Om ECI-filer
uuid: 124d8ab1-933b-4a1b-992a-919f3d799460
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Om ECI-filer{#about-eci-files}

Förutom listor över återkallade certifikat måste du även regelbundet uppdatera filer i det inbäddade gemensamma gränssnittet (ECI). När Adobe lägger till stöd för en ny Primetime DRM-klientplattform (till exempel: iOS, Android, Windows Flash Player osv.) skapas en ny ECI-post. För att stödja personaliseringen av den här klienten måste en motsvarande ECI-post finnas på Individualization Server.

Eftersom det inte är särskilt vanligt att nya Primetime DRM-klienter släpps kommer Adobe att släppa uppdaterade ECI-data vid behov. Adobe kommer regelbundet att samla in ECI-filer och lagra dem på nedanstående plats för distribution:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

Filen [!DNL Latest.txt] innehåller URL:en till den senaste CRL-distributionsfilen.

Adobe kommer att skapa ECI zip-filen på det sätt som beskrivs nedan:

Mappstruktur:

```
ECI\*
```

Innehållet i mappen kommer att rekursiveras:

```
zip -R ECI ECI.zip
```

Ett OpenSSL SHA-256-sammandrag beräknas av zip-filen:

```
openssl dgst -sha256 -hex ECI.zip
```

ZIP-filen kommer att byta namn så att den innehåller arkivdatumet samt SHA-256-sammanfattningen:

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

Exempel:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

Du bör regelbundet kontrollera platsen ovan för uppdaterade ECI-filer.

Utför följande process för installation efter hämtning:

1. Anteckna SHA-256-sammanfattningen och beräkna om den med OpenSSL eller ett motsvarande verktyg.
1. Jämför den med den som anges i filnamnet.
1. Byt namn på filen till [!DNL ECI.zip].
1. Zippa upp katalogen [!DNL ECI].
1. Ersätt den gamla ECI-katalogen med den nya.
1. Starta om Individualization-servern.

