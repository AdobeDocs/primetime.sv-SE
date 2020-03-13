---
description: Processen för annonsinfogning video-on-demand (VOD) består av faserna för annonsupplösning, annonsinfogning och annonsuppspelning. För annonsspårning måste webbläsarens TVSDK informera en fjärrspårningsserver om uppspelningsförloppet för varje annons. Om det uppstår oväntade situationer krävs lämpliga åtgärder.
seo-description: Processen för annonsinfogning video-on-demand (VOD) består av faserna för annonsupplösning, annonsinfogning och annonsuppspelning. För annonsspårning måste webbläsarens TVSDK informera en fjärrspårningsserver om uppspelningsförloppet för varje annons. Om det uppstår oväntade situationer krävs lämpliga åtgärder.
seo-title: Annonsinfogning och failover för VOD
title: Annonsinfogning och failover för VOD
uuid: 33f7aad5-fc4f-459d-8c29-01ba1353dfcc
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Annonsinfogning och failover för VOD{#advertising-insertion-and-failover-for-vod}

Processen för annonsinfogning video-on-demand (VOD) består av faserna för annonsupplösning, annonsinfogning och annonsuppspelning. För annonsspårning måste webbläsarens TVSDK informera en fjärrspårningsserver om uppspelningsförloppet för varje annons. Om det uppstår oväntade situationer krävs lämpliga åtgärder.

## Ad-resolving phase {#section_F562CD6D0EF04AA9A0A3C0176A4EC340}

Webbläsarens TVSDK kontaktar en annonsleveranstjänst, t.ex. Adobe Primetimes annonsbeslut, och försöker hämta den primära spellistfilen som motsvarar annonsens videoström. Under reklamlösningsfasen gör Browser TVSDK ett HTTP-anrop till fjärr-annonsservern och tolkar serverns svar.

Browser TVSDK stöder följande typer av annonseringsleverantörer:

* Metadata och leverantör

   Annonsdata kodas i JSON-filer med oformaterad text.
* Adobe Primetimes annonsleverantör

   Browser TVSDK skickar en begäran, inklusive en uppsättning parametrar för målinriktning och ett resursidentifieringsnummer, till Adobe Primetimes server för annonsbeslut. Adobe Primetimes annonsbeslut besvaras med ett SMIL-dokument (synkroniserat multimedieintegrationsspråk) som innehåller den annonseringsinformation som krävs.

   En av följande redundanssituationer kan uppstå under den här fasen:

   * Det går inte att hämta data på grund av bl.a. bristande anslutning eller fel på serversidan, t.ex. att en resurs inte kan hittas osv.
   * Data hämtades, men formatet är ogiltigt.

      Detta kan inträffa till exempel på grund av att tolkningen av inkommande data misslyckades.
   Webbläsarens TVSDK skickar ett varningsmeddelande om felet och bearbetningen fortsätter.

## Fas för annonsinfogning {#section_88A0E4FA12394717A9D85689BD11D59F}

Webbläsarens TVSDK infogar det alternativa innehållet (annonserna) på tidslinjen som motsvarar huvudinnehållet.

När annonslösningsfasen är klar har Browser TVSDK en ordnad lista över annonsresurser som grupperats i annonsbrytningar. Varje annonsbrytning placeras på huvudinnehållets tidslinje med ett starttidsvärde som uttrycks i millisekunder (ms). Varje annons i en annonsbrytning har en duration-egenskap som också uttrycks i ms. Annonserna i en annonsbrytning är sammankopplade, den ena efter den andra. Följaktligen är längden på en annonsbrytning lika med summan av varaktigheten för de enskilda dispositionsannonserna.

Redundans kan uppstå i den här fasen med konflikter som kan uppstå på tidslinjen när annonsinfogningen infogas. För specifika kombinationer av starttids-/varaktighetsvärden för annonsavbrott kan annonssegmenten överlappa varandra. Överlappningen inträffar när den sista delen av en annonsbrytning korsar början av den första annonsbrytningen i nästa annonsbrytning. I dessa situationer tar Browser TVSDK bort den senare annonsuppdelningen och fortsätter med annonsinfogningen med nästa objekt i listan tills alla annonsuppbrytningar infogas eller tas bort.

Webbläsarens TVSDK skickar ett varningsmeddelande om felet och bearbetningen fortsätter.

## Ad-uppspelningsfas {#section_7B0073BE9A744C74929263182C1243FC}

Webbläsaren TVSDK hämtar annonssegmenten och återger dem på enhetens skärm.

I det här skedet har webbläsarens TVSDK löst annonser, placerat dem på tidslinjen och försökt återge innehållet på skärmen.

Följande huvudfelklasser kan förekomma i den här fasen:

* Fel vid anslutning till värdservern
* Fel vid hämtning av manifestfilen
* Fel vid hämtning av mediesegment

För alla tre felklasserna vidarebefordrar webbläsaren TVSDK utlösta händelser till ditt program, inklusive:

* Meddelandehändelser som utlöses när en redundans inträffar.
* Meddelandehändelser när profilen ändras på grund av redundansalgoritmen.
* Meddelandehändelser utlöses när alla alternativ för växling vid fel har beaktats och inga ytterligare åtgärder kan vidtas automatiskt.

   Programmet måste vidta rätt åtgärd.

Oavsett om fel uppstår eller inte visas ett meddelande i webbläsaren om när en annonsbrytning börjar och när den är klar. Om segment inte kunde hämtas kan det dock finnas luckor i tidslinjen. När mellanrummen är tillräckligt stora kan värdena i spelhuvudet och den rapporterade annonsen visa avbrott.
