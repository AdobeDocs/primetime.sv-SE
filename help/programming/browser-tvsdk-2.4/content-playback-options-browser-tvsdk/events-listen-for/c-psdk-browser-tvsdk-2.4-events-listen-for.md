---
description: Händelser från webbläsarens TVSDK visar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, t.ex. att en video börjar spelas upp eller åtgärder som utförs implicit, t.ex. att en annons slutförs.
title: Lyssna efter händelser för Primetime Player
exl-id: e16fa356-5286-4cae-b7ce-74a2e8093d62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Översikt {#listen-for-primetime-player-events-overview}

Händelser från webbläsarens TVSDK visar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, t.ex. att en video börjar spelas upp eller åtgärder som utförs implicit, t.ex. att en annons slutförs.

Eftersom ditt program behöver svara på många av dessa händelser måste du implementera händelsehanteringsrutiner och registrera dessa rutiner med Browser TVSDK. Rutinerna anropar webbläsarens TVSDK-metoder för att svara korrekt.

Här finns ytterligare information om händelser:

* Videouppspelningens realtidskaraktär kräver asynkron (icke-blockerande) aktivitet för många webbläsaråtgärder i TVSDK.
* Webbläsarens TVSDK stöder en händelsestyrd videospelare.

   Den innehåller händelser som motsvarar alla viktiga steg i uppspelningsprocessen. Du registrerar dessa händelser med plattformens händelsemekanism och skapar händelsehanterare som anropas när dessa händelser inträffar. *`Event Handlers`* kallas också för callback-rutiner eller händelseavlyssnare. Browser TVSDK innehåller ett komplett antal metoder som kan användas av händelsehanterarna.
* Programmet initierar vanligtvis icke-blockerande åtgärder, som att begära att en video börjar spelas upp.

   Webbläsaren TVSDK kommunicerar asynkront med programmet genom att skicka händelser, till exempel när videon börjar spelas upp och en händelse när videon är klar. Andra händelser kan indikera statusändringar i spelaren och feltillstånd. Dina händelsehanterare vidtar lämpliga åtgärder.
