---
description: TVSDK infogar det alternativa innehållet (annonserna) på tidslinjen som motsvarar huvudinnehållet.
title: Fas för annonsinfogning
exl-id: bad246e9-ff2b-4584-a320-826385bb0e6d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Fas för annonsinfogning{#ad-insertion-phase}

TVSDK infogar det alternativa innehållet (annonserna) på tidslinjen som motsvarar huvudinnehållet.

När annonslösningsfasen är klar har TVSDK en ordnad lista över annonsresurser som grupperas i annonsbrytningar. Varje annonsbrytning placeras på huvudinnehållets tidslinje med ett starttidsvärde som uttrycks i millisekunder (ms). Varje annons i en annonsbrytning har en duration-egenskap som också uttrycks i ms. Annonserna i en annonsbrytning är sammankopplade, den ena efter den andra. Följaktligen är längden på en annonsbrytning lika med summan av varaktigheten för de enskilda dispositionsannonserna.

Redundans kan uppstå i den här fasen med konflikter som kan uppstå på tidslinjen när annonsinfogningen infogas. För specifika kombinationer av starttids-/varaktighetsvärden för annonsavbrott kan annonssegmenten överlappa varandra. Överlappningen inträffar när den sista delen av en annonsbrytning korsar början av den första annonsbrytningen i nästa annonsbrytning. I dessa situationer tar TVSDK bort den efterföljande annonsuppdelningen och fortsätter med annonsinfogningen med nästa objekt i listan tills alla annonsuppbrytningar infogas eller tas bort.

TVSDK skickar ett varningsmeddelande om felet och bearbetningen fortsätter.
