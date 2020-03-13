---
description: Händelser från TVSDK indikerar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, till exempel att en video börjar spelas upp eller åtgärder som utförs implicit, till exempel att en annons slutförs.
seo-description: Händelser från TVSDK indikerar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, till exempel att en video börjar spelas upp eller åtgärder som utförs implicit, till exempel att en annons slutförs.
seo-title: Lyssna efter händelser för Primetime Player
title: Lyssna efter händelser för Primetime Player
uuid: e72782bf-9d26-4285-85e4-fd4d803c1bbe
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Översikt {#listen-for-primetime-player-events-overview}

Händelser från TVSDK indikerar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, till exempel att en video börjar spelas upp eller åtgärder som utförs implicit, till exempel att en annons slutförs.

Eftersom ditt program behöver svara på många av dessa händelser måste du implementera händelsehanteringsrutiner och registrera dessa rutiner med TVSDK. Rutinerna anropar de relevanta TVSDK-metoderna för att svara på lämpligt sätt.

Här finns ytterligare information om händelser:

* Videouppspelningens realtidskaraktär kräver asynkron (icke-blockerande) aktivitet för många TVSDK-åtgärder.
* TVSDK stöder en händelsestyrd videospelare.

   Den innehåller händelser som motsvarar alla viktiga steg i uppspelningsprocessen. Du registrerar dessa händelser med plattformens händelsemekanism och skapar händelsehanterare som anropas när dessa händelser inträffar. *`Event Handlers`* kallas också för callback-rutiner eller händelseavlyssnare. TVSDK innehåller ett komplett antal metoder som kan användas av händelsehanterarna.
* Programmet initierar vanligtvis icke-blockerande åtgärder, som att begära att en video börjar spelas upp.

   TVSDK kommunicerar asynkront med programmet genom att skicka händelser, som när videon börjar spelas upp och en händelse när videon är klar. Andra händelser kan indikera statusändringar i spelaren och feltillstånd. Dina händelsehanterare vidtar lämpliga åtgärder.

