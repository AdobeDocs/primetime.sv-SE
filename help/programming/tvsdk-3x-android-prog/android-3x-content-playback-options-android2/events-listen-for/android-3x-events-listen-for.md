---
description: Händelser från TVSDK visar spelarens status, fel som inträffar, slutförandet av åtgärder som du har begärt, t.ex. att en video börjar spelas upp eller åtgärder som utförs implicit, t.ex. att en annons slutförs.
title: Lyssna efter händelser för Primetime Player
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Ökning {#listen-for-primetime-player-events-overview}

Händelser från TVSDK visar spelarens status, fel som inträffar, slutförandet av åtgärder som du har begärt, t.ex. att en video börjar spelas upp eller åtgärder som utförs implicit, t.ex. att en annons slutförs.

Eftersom ditt program behöver svara på många av dessa händelser måste du implementera händelsehanteringsrutiner och registrera dessa rutiner med TVSDK. Rutinerna anropar de relevanta TVSDK-metoderna för att svara på lämpligt sätt.

Mer information om händelser:

* Videouppspelningens realtidskaraktär kräver asynkron (icke-blockerande) aktivitet för många TVSDK-åtgärder.
* TVSDK stöder en händelsestyrd videospelare.

  Den innehåller händelser som motsvarar alla viktiga steg i uppspelningsprocessen. Du registrerar dessa händelser med plattformens händelsemekanism och skapar händelsehanterare som anropas när dessa händelser inträffar. *`Event Handlers`* kallas också för callback-rutiner eller händelseavlyssnare. TVSDK innehåller ett komplett antal metoder som kan användas av händelsehanterarna.
* Programmet initierar vanligtvis icke-blockerande åtgärder, som att begära att en video börjar spelas upp.

  TVSDK kommunicerar asynkront med programmet genom att skicka händelser, som när videon börjar spelas upp och en händelse när videon är klar. Andra händelser kan indikera statusändringar i spelaren och feltillstånd. Dina händelsehanterare vidtar lämpliga åtgärder.
