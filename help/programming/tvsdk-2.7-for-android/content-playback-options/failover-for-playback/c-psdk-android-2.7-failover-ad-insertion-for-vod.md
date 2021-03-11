---
description: Processen för annonsinfogning video-on-demand (VOD) består av faserna för annonsupplösning, annonsinfogning och annonsuppspelning. För annonsspårning måste TVSDK informera en fjärrspårningsserver om uppspelningsförloppet för varje annons. När oväntade situationer uppstår vidtar TVSDK lämpliga åtgärder.
title: Annonsinfogning och failover för VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# Annonsinfogning och failover för VOD {#advertising-insertion-and-failover-for-vod}

Processen för annonsinfogning video-on-demand (VOD) består av faserna för annonsupplösning, annonsinfogning och annonsuppspelning. För annonsspårning måste TVSDK informera en fjärrspårningsserver om uppspelningsförloppet för varje annons. När oväntade situationer uppstår vidtar TVSDK lämpliga åtgärder.

## Ad-resolving phase {#section_5DD3A7DA79E946298BFF829A60202E1C}

TVSDK kontaktar en annonsleveranstjänst, t.ex. Adobe Primetime annonsbeslut, och försöker hämta den primära spellistfilen som motsvarar annonsens videoström. Under reklamlösningsfasen gör TVSDK ett HTTP-anrop till den fjärranslutna annonsservern och tolkar serverns svar.

TVSDK har stöd för följande typer av annonsleverantörer:

* Metadata och leverantör

   Annonsdata kodas i JSON-filer med oformaterad text.
* Annonsleverantör för Primetime-annonsbeslut

   TVSDK skickar en begäran, inklusive en uppsättning parametrar för målinriktning och ett resursidentifieringsnummer, till huvudservern för Primetime-annonsbeslut. Primetime-annonseringsbeslut svarar med ett synkroniserat SMIL-dokument (multimedia integration language) som innehåller den annonsinformation som krävs.
* Anordnare av anpassade annonser

   Hanterar situationen där annonser bränns in i strömmen från serversidan. TVSDK utför inte den faktiska annonsinfogningen, men det måste hålla reda på de annonser som infogades på serversidan. Den här providern ställer in annonsmarkörerna som TVSDK använder för att utföra annonsspårningen.

En av följande redundanssituationer kan uppstå under den här fasen:

* Det går inte att hämta data eftersom det t.ex. inte går att ansluta till servern eller på grund av fel på serversidan, t.ex. att en resurs inte kan hittas.
* Data hämtades, men formatet är ogiltigt.

   Detta kan inträffa till exempel på grund av att tolkningen av inkommande data misslyckades.

TVSDK skickar ett varningsmeddelande om felet och bearbetningen fortsätter.

## Ad-insertion phase {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

TVSDK infogar det alternativa innehållet (annonserna) på tidslinjen som motsvarar huvudinnehållet.

När annonslösningsfasen är klar har TVSDK en ordnad lista över annonsresurser som grupperas i annonsbrytningar. Varje annonsbrytning placeras på huvudinnehållets tidslinje med ett starttidsvärde som uttrycks i millisekunder (ms). Varje annons i en annonsbrytning har en duration-egenskap som också uttrycks i ms. Annonserna i en annonsbrytning är kedjade, och därför är längden på en annonsbrytning lika med summan av varaktigheten för de enskilda dispositionsannonserna.

Redundans kan uppstå i den här fasen med konflikter som kan uppstå på tidslinjen när annonsinfogningen infogas. För specifika kombinationer av starttids-/varaktighetsvärden för annonsavbrott kan annonssegmenten överlappa varandra. Den här överlappningen inträffar när den sista delen av en annonsbrytning korsar början av den första annonsbrytningen i nästa annonsbrytning. I dessa situationer tar TVSDK bort den efterföljande annonsuppdelningen och fortsätter med annonsinfogningen med nästa objekt i listan tills alla annonsuppbrytningar infogas eller tas bort.

TVSDK skickar ett varningsmeddelande om felet och bearbetningen fortsätter.

## Annonsuppspelningsfas {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

TVSDK hämtar annonssegmenten och återger dem på enhetens skärm.

Nu har TVSDK löst annonser, positionerat annonserna på tidslinjen och försökt återge innehållet på skärmen.

Följande huvudklasser av fel kan uppstå under följande faser:

* Vid anslutning till värdservern.
* När manifestfilen hämtas.
* När mediesegmenten hämtas.

TVSDK skickar de utlösta händelserna till ditt program, inklusive meddelandehändelser som utlöses när:

* En failover sker.
* Profilen ändras på grund av redundansalgoritmen.
* Alla alternativ för växling vid fel har beaktats och ingen ytterligare åtgärd kan vidtas automatiskt.

   Programmet måste vidta rätt åtgärd.

Oavsett om fel inträffar anropar TVSDK `onAdBreakComplete` för var `onAdBreakStart` och `onAdComplete` för var `onAdStart`. Om segment inte kunde hämtas kan det dock finnas luckor i tidslinjen. När mellanrummen är tillräckligt stora kan värdena i spelhuvudet och den rapporterade annonsen visa avbrott.
