---
description: TVSDK kan identifiera ändrad uppspelningsinformation i mastermanifest m3u8 för direktuppspelning och uppdatera uppspelningsinformationen medan direktuppspelningen pågår. TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från huvudmanifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.
seo-description: TVSDK kan identifiera ändrad uppspelningsinformation i mastermanifest m3u8 för direktuppspelning och uppdatera uppspelningsinformationen medan direktuppspelningen pågår. TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från huvudmanifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.
seo-title: Live master-manifest update
title: Live master-manifest update
uuid: 44f8adc2-0538-4c5d-8e39-55f661d8540b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Live master-manifest update{#live-master-manifest-update}

TVSDK kan identifiera ändrad uppspelningsinformation i mastermanifest m3u8 för direktuppspelning och uppdatera uppspelningsinformationen medan direktuppspelningen pågår. TVSDK stöder en dynamisk uppsättning bithastighetsprofiler när profilerna visas eller försvinner från huvudmanifestet, inklusive icke-överlappande profilbithastigheter mellan uppdateringar.

Följande funktioner stöds:

* Profilantal (öka eller minska)
* Profilbithastigheter (överlappande eller inte överlappande)
* Profiler med URL:er på samma (eller olika) servrar
* Alla redundansstrukturer

Alla följande villkor måste vara uppfyllda:

* Strömmen är live.
* Både tid och tagg ändras.
* All återgivningsinformation är densamma (förutom att URL:er kan variera).
* DRM-åtkomstinformationen är densamma.
* Segment paketeras runt samma PTS och bildrutegränser i ett litet felintervall.

## Live master-manifest update architecture {#section_32254A0F684B4960ACC33BF6B1AEF6F1}

Här följer information och exempel om hur TVSDK kan hantera uppdaterade huvudmanifest.

Som standard är den här funktionen inaktiverad. Om programmet aktiveras genom att en uppdateringsfrekvens anges i minuter utförs följande steg efter varje uppdateringsintervall:

1. TVSDK kontrollerar huvudmanifestets senaste ändringsdatum och -tagg för att avgöra om filen har uppdaterats.

   Om både tid och tagg har ändrats betraktas filen som ändrad.
1. TVSDK tolkar och analyserar det nya manifestet och vidtar lämpliga åtgärder utifrån uppdateringens karaktär.
1. Om den aktuella uppspelningsbithastigheten matchar bithastigheten för det ändrade manifestet växlar TVSDK till den nya profilen.

   Den nya profilen kan komma från en annan server eller samma server, med samma bithastighet. I det här fallet är övergången mjuk.
1. Om den aktuella uppspelningsbithastigheten inte längre finns i det nya manifestet försöker TVSDK hitta en bithastighet i den aktuella profilen som också finns i det nya manifestet.

   * Om en matchning hittas växlar spelaren först till den matchande bithastighetsprofilen i det befintliga manifestet och växlar till den matchande bithastighetsprofilen i det uppdaterade manifestet. Detta garanterar att övergången blir jämn.
   * Om det inte finns någon gemensam bithastighet mellan det föregående och det nya manifestet, eller om TVSDK inte kan växla till den bithastighet som matchar, växlar TVSDK direkt till den lägsta bithastighetsprofilen i det nya manifestet och använder ABR för att växla till en tillåten bithastighet baserat på bandbredd. Detta kan orsaka en viss uppspelningsavvikelse, men bör få minimal effekt.

1. Om uppdateringen lyckas skickar TVSDK en `MediaPlayerItemEvent.MASTER_UPDATED` händelse.
1. Om uppdateringen inte lyckas fortsätter uppspelningen med konfigurationen från före den här uppdateringen.

### Exempel 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

Följande bithastigheter är direktsändning:

* 500k
* 900k
* 2100k

2100k-strömmen har vissa problem, så den måste startas om. Huvudmanifestet uppdateras till att endast innehålla 500 kB och 900 kB. Kort därefter kommer användare som tittar på det här programmet vid 2 100 kB att uppleva en nedväxling av bithastigheten till 900 kB. Användare som tittar på 900 kB fortsätter att titta på 900 kB. Senare återupptas 2 100 kB-strömmen och läggs tillbaka i huvudmanifestet. En stund senare ändras de användare som tittar på 900 kB och har bandbredden till 2 100 kB.

### Exempel 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

Följande bithastigheter är direktsändning:

* 500k
* 900k
* 2100k

Alla dessa bithastigheter måste startas om. Två tidsströmmar har konfigurerats för detta, 400 kB och 1 500 kB. Användarna växlas till 400 kB, vilket är den lägsta bithastigheten i den nya konfigurationen. Vissa användare växlar till 1 500 kB när deras bandbredd är tillräcklig. Senare är de tre bithastigheterna säkerhetskopierade och huvudmanifestet uppdateras. Användare växlar automatiskt tillbaka till att titta på vid 500 kB, vilket är den lägsta bandbredden i det reviderade (ursprungliga) manifestet. Under en längre tid växlas användarna till den högsta bandbredd (900 kB eller 1 200 kB) som deras nätverk tillåter.

## Använd uppdatering av mastermanifest live {#section_34AC4A9751DB4B7C8561302C6A59A1C4}

Du kan aktivera den här funktionen och söka efter relaterade händelser.

1. Om du vill aktivera uppdateringar av mastermanifestet anger du uppdateringsfrekvensen (i minuter) genom att ange `NetworkConfiguration.masterUpdateInterval` egenskapen.
1. Du kan också spåra lyckade manifestuppdateringar genom att avlyssna `MediaPlayerItemEvent.MASTER_UPDATED` händelsen.

