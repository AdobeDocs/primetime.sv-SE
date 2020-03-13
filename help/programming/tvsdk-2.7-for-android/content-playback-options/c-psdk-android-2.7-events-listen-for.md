---
description: Händelser från TVSDK visar spelarens status, fel som inträffar, slutförandet av åtgärder som du har begärt, till exempel att en video börjar spelas upp eller åtgärder som utförs implicit, till exempel att en annons slutförs.
seo-description: Händelser från TVSDK visar spelarens status, fel som inträffar, slutförandet av åtgärder som du har begärt, till exempel att en video börjar spelas upp eller åtgärder som utförs implicit, till exempel att en annons slutförs.
seo-title: Lyssna efter händelser för Primetime Player
title: Lyssna efter händelser för Primetime Player
uuid: bd0a428c-fa51-41a6-950a-9d6843c6e177
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Översikt {#listen-for-primetime-player-events-overview}

Händelser från TVSDK visar spelarens status, fel som inträffar, slutförandet av åtgärder som du har begärt, till exempel att en video börjar spelas upp eller åtgärder som utförs implicit, till exempel att en annons slutförs.

Eftersom ditt program behöver svara på många av dessa händelser måste du implementera händelsehanteringsrutiner och registrera dessa rutiner med TVSDK. Rutinerna anropar de relevanta TVSDK-metoderna för att svara på lämpligt sätt.

Mer information om händelser:

* Videouppspelningens realtidskaraktär kräver asynkron (icke-blockerande) aktivitet för många TVSDK-åtgärder.
* TVSDK stöder en händelsestyrd videospelare.

   Den innehåller händelser som motsvarar alla viktiga steg i uppspelningsprocessen. Du registrerar dessa händelser med plattformens händelsemekanism och skapar händelsehanterare som anropas när dessa händelser inträffar. *`Event Handlers`* kallas också för callback-rutiner eller händelseavlyssnare. TVSDK innehåller ett komplett antal metoder som kan användas av händelsehanterarna.
* Programmet initierar vanligtvis icke-blockerande åtgärder, som att begära att en video börjar spelas upp.

   TVSDK kommunicerar asynkront med programmet genom att skicka händelser, som när videon börjar spelas upp och en händelse när videon är klar. Andra händelser kan indikera statusändringar i spelaren och feltillstånd. Dina händelsehanterare vidtar lämpliga åtgärder.