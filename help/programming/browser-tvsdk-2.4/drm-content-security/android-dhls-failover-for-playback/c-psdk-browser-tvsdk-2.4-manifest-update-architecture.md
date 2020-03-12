---
description: Här är information och exempel på hur webbläsaren TVSDK kan hantera uppdaterade mallmanifest.
seo-description: Här är information och exempel på hur webbläsaren TVSDK kan hantera uppdaterade mallmanifest.
seo-title: Live master-manifest update architecture
title: Live master-manifest update architecture
uuid: 6f253502-8dec-4b42-9ee1-99ad9bfd6080
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Live master-manifest update architecture{#live-master-manifest-update-architecture}

Här är information och exempel på hur webbläsaren TVSDK kan hantera uppdaterade mallmanifest.

Som standard är den här funktionen inaktiverad. Om programmet aktiveras genom att en uppdateringsfrekvens anges i minuter utförs följande steg efter varje uppdateringsintervall:

1. Webbläsarens TVSDK kontrollerar mallmanifestets senaste ändringsdatum och -tagg för att avgöra om filen har uppdaterats.

   Om både tid och tagg har ändrats betraktas filen som ändrad.
1. Browser TVSDK tolkar och analyserar det nya manifestet och vidtar lämpliga åtgärder utifrån uppdateringens karaktär.
1. Om den aktuella uppspelningsbithastigheten matchar bithastigheten för det ändrade manifestet växlar webbläsarens TVSDK till den nya profilen.

   Den nya profilen kan komma från en annan server eller samma server, med samma bithastighet. I det här fallet är övergången mjuk.
1. Om den aktuella uppspelningsbithastigheten inte längre finns i det nya manifestet försöker webbläsaren TVSDK hitta en bithastighet i den aktuella profilen som också finns i det nya manifestet.

   * Om en matchning hittas växlar spelaren först till den matchande bithastighetsprofilen i det befintliga manifestet och växlar till den matchande bithastighetsprofilen i det uppdaterade manifestet. Detta garanterar att övergången blir jämn.
   * Om det inte finns någon gemensam bithastighet mellan det föregående och det nya manifestet, eller om webbläsarens TVSDK inte kan växla till den bithastighet som matchar, växlar webbläsarens TVSDK direkt till den lägsta bithastighetsprofilen i det nya manifestet och använder ABR för att växla till en tillåten bithastighet baserat på bandbredd. Detta kan orsaka en viss uppspelningsavvikelse, men bör få minimal effekt.

1. Om uppdateringen lyckas skickar webbläsaren TVSDK en `MediaPlayerItemEvent.MASTER_UPDATED` händelse.
1. Om uppdateringen inte lyckas fortsätter uppspelningen med konfigurationen från före den här uppdateringen.

## Exempel 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

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

<!-- 

WRITER: Add relref to api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#MASTER_UPDATED

 -->

