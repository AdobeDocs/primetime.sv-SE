---
description: Processen för annonsinfogning video-on-demand (VOD) består av faserna för annonsupplösning, annonsinfogning och annonsuppspelning. För annonsspårning måste TVSDK informera en fjärrspårningsserver om uppspelningsförloppet för varje annons. Om det uppstår oväntade situationer krävs lämpliga åtgärder.
seo-description: Processen för annonsinfogning video-on-demand (VOD) består av faserna för annonsupplösning, annonsinfogning och annonsuppspelning. För annonsspårning måste TVSDK informera en fjärrspårningsserver om uppspelningsförloppet för varje annons. Om det uppstår oväntade situationer krävs lämpliga åtgärder.
seo-title: Annonsinfogning och failover för VOD
title: Annonsinfogning och failover för VOD
uuid: 98505f63-ac43-4ff5-9f7b-895b6135df47
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Annonsinfogning och failover för VOD{#advertising-insertion-and-failover-for-vod}

Processen för annonsinfogning video-on-demand (VOD) består av faserna för annonsupplösning, annonsinfogning och annonsuppspelning. För annonsspårning måste TVSDK informera en fjärrspårningsserver om uppspelningsförloppet för varje annons. Om det uppstår oväntade situationer krävs lämpliga åtgärder.

## Ad-resolving phase {#section_0D45C6094D724B55868B48F9A3557A8B}

TVSDK kontaktar en annonsleveranstjänst, till exempel Adobe Primetimes annonsbeslut, och försöker hämta den primära spellistfilen som motsvarar annonsens videoström. Under reklamlösningsfasen gör TVSDK ett HTTP-anrop till den fjärranslutna annonsservern och tolkar serverns svar.

TVSDK har stöd för följande typer av annonsleverantörer:

* Metadata och leverantör

   Annonsdata kodas i JSON-filer med oformaterad text.
* Annonsleverantör för Primetime-annonsbeslut

   TVSDK skickar en begäran, inklusive en uppsättning parametrar för målinriktning och ett resursidentifieringsnummer, till den bakomliggande servern för Primetime-annonsbeslut. Primetime-annonsbeslut svarar med ett SMIL-dokument (synkroniserat multimedieintegrationsspråk) som innehåller den annonseringsinformation som krävs.

En av följande redundanssituationer kan uppstå under den här fasen:

* Det går inte att hämta data på grund av bl.a. bristande anslutning eller fel på serversidan, t.ex. att en resurs inte kan hittas osv.
* Data hämtades, men formatet är ogiltigt.

   Detta kan inträffa till exempel på grund av att tolkningen av inkommande data misslyckades.

TVSDK skickar ett varningsmeddelande om felet och bearbetningen fortsätter.

## Fas för annonsinfogning {#section_1B18E8B5768B4873B3346294175B7340}

TVSDK infogar det alternativa innehållet (annonserna) på tidslinjen som motsvarar huvudinnehållet.

När annonslösningsfasen är klar har TVSDK en ordnad lista över annonsresurser som grupperas i annonsbrytningar. Varje annonsbrytning placeras på huvudinnehållets tidslinje med ett starttidsvärde som uttrycks i millisekunder (ms). Varje annons i en annonsbrytning har en duration-egenskap som också uttrycks i ms. Annonserna i en annonsbrytning är sammankopplade, den ena efter den andra. Följaktligen är längden på en annonsbrytning lika med summan av varaktigheten för de enskilda dispositionsannonserna.

Redundans kan uppstå i den här fasen med konflikter som kan uppstå på tidslinjen när annonsinfogningen infogas. För specifika kombinationer av starttids-/varaktighetsvärden för annonsavbrott kan annonssegmenten överlappa varandra. Överlappningen inträffar när den sista delen av en annonsbrytning korsar början av den första annonsbrytningen i nästa annonsbrytning. I dessa situationer tas den efterföljande annonbrytningen bort och annonsinfogningsprocessen fortsätter med nästa objekt i listan tills alla annonbrytningar infogas eller tas bort.

TVSDK skickar ett varningsmeddelande om felet och bearbetningen fortsätter.

## Ad-uppspelningsfas {#section_64777BD2CDA84EACB0A4EA6D68367CF5}

TVSDK hämtar annonssegmenten och återger dem på enhetens skärm.

Nu har TVSDK löst annonser, placerat dem på tidslinjen och försökt återge innehållet på skärmen.

Följande huvudfelklasser kan förekomma i den här fasen:

* Fel vid anslutning till värdservern
* Fel vid hämtning av manifestfilen
* Fel vid hämtning av mediesegment

För alla tre felklasserna vidarebefordrar TVSDK utlösta händelser till ditt program, inklusive:

* Meddelandehändelser som utlöses när en redundans inträffar.
* Meddelandehändelser när profilen ändras på grund av redundansalgoritmen.
* Meddelandehändelser utlöses när alla alternativ för växling vid fel har beaktats och inga ytterligare åtgärder kan vidtas automatiskt.

   Programmet måste vidta rätt åtgärd.

Oavsett om fel inträffar eller inte, anropar TVSDK `AdBreakPlaybackEvent.AD_BREAK_COMPLETE` for each `AdBreakPlaybackEvent.AD_BREAK_STARTED` och `AdPlaybackEvent.AD_COMPLETED` for each `AdPLaybackEvent.AD_STARTED`. Om segment inte kunde hämtas kan det dock finnas luckor i tidslinjen. När mellanrummen är tillräckligt stora kan värdena i spelhuvudet och den rapporterade annonsen visa avbrott.
