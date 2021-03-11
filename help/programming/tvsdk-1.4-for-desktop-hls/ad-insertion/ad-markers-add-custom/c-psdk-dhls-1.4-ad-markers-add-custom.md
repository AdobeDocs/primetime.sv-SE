---
description: Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.
title: Lägga till egna annonsmärken
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Översikt {#add-custom-ad-markers-overview}

Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.

Den här funktionen är mest användbar när innehåll spelas in, till exempel från en live-händelse, och resultatet av inspelningen är en HLS-ström. Inspelningen innehåller huvudinnehåll och reklamrelaterat innehåll i en HLS-video-on-demand-ström (VOD). Inspelningsprocessen håller inte reda på de annonsrelaterade segmenten, så informationen som är relaterad till annonsernas placering i huvudinnehållet går förlorad.

Ni kan kanske få den information som är relaterad till positioneringen av annonsinnehållsperioderna från andra källor utanför bandet, som externa CMS-system. Du kan definiera anpassade markörer, genom vilka den här out-of-band-informationen kan skickas till undersystemet för tidslinjehantering. Avsikten är att markera de avsnitt av innehållet som matchar det angivna annonsrelaterade innehållet på ett sådant sätt att alla annonsspecifika uppspelningshändelser utlöses på samma sätt som om dessa anpassade annonsperioder uttryckligen placerades på spelarens tidslinje.

Annonsuppföljning hanteras inte internt av TVSDK, till exempel när annonser löses genom Adobe Primetime annonsbeslut (tidigare Auditude). TVSDK innehåller dock följande abstraktioner som definierar hur annonsrelaterat innehåll visas på tidslinjen:

* Annonsbrytning

   En annonsbrytning är en ordnad lista med enskilda annonser i följd.
* En enskild annons

Uppspelningshändelser utlöses separat för annonsbrytningar och annonser vid start- och slutpunkten för varje annons.

TVSDK skickar annonsuppföljningshändelser till ditt program, så att du kan implementera din egen spårningslogik. Om du ställer in anpassade annonsmarkörer får du händelserna `AD_BREAK_STARTED`, `AD_STARTED`, `AD_PROGRESS`, `AD_COMPLETED` och `AD_BREAK_COMPLETED`.