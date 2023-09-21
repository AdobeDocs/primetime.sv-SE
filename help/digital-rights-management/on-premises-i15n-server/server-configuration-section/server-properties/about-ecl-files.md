---
title: Om ECI-filer
description: Om ECI-filer
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Om ECI-filer{#about-eci-files}

Förutom listor över återkallade certifikat måste du även regelbundet uppdatera filer i det inbäddade gemensamma gränssnittet (ECI). När Adobe lägger till stöd för en ny Primetime DRM-klientplattform (t.ex. iOS, Android, Windows Flash Player) skapas en ny ECI-post. För att stödja personaliseringen av den här klienten måste en motsvarande ECI-post finnas på Individualization Server.

Eftersom det inte är särskilt vanligt att nya Primetime DRM-klienter släpps kommer Adobe att släppa uppdaterade ECI-data vid behov. Adobe kommer regelbundet att samla in ECI-filer och lagra dem på nedanstående plats för distribution:

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

The [!DNL Latest.txt] filen innehåller URL:en till den senaste CRL-distributionsfilen.

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

Till exempel:

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

Du bör regelbundet kontrollera platsen ovan för uppdaterade ECI-filer.

Utför följande process för installation efter hämtning:

1. Anteckna SHA-256-sammanfattningen och beräkna om den med OpenSSL eller ett motsvarande verktyg.
1. Jämför den med den som anges i filnamnet.
1. Byt namn på filen till [!DNL ECI.zip].
1. Zippa upp [!DNL ECI] katalog.
1. Ersätt den gamla ECI-katalogen med den nya.
1. Starta om Individualization-servern.
