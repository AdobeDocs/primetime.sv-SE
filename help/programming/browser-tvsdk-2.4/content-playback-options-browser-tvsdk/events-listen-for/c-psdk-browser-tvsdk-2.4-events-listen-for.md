---
description: Händelser från webbläsarens TVSDK visar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, t.ex. att en video börjar spelas upp eller åtgärder som utförs implicit, t.ex. att en annons slutförs.
seo-description: Händelser från webbläsarens TVSDK visar spelarens tillstånd, fel som inträffar, slutförandet av åtgärder som du har begärt, t.ex. att en video börjar spelas upp eller åtgärder som utförs implicit, t.ex. att en annons slutförs.
seo-title: Lyssna efter händelser för Primetime Player
title: Lyssna efter händelser för Primetime Player
uuid: 7b7c28ac-22ae-46a3-bbeb-bef1b04baeb3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '304'
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

