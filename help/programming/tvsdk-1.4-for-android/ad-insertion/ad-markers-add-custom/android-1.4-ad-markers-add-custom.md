---
description: Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.
seo-description: Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.
seo-title: Lägga till egna annonsmärken
title: Lägga till egna annonsmärken
uuid: 5d8c8aaa-a4e7-499d-b70e-5c72007ec269
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Översikt {#add-custom-ad-markers-overview}

Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.

Den här funktionen är mest användbar när innehåll spelas in, till exempel från en live-händelse, och resultatet av inspelningen är en HLS-ström. Inspelningen innehåller huvudinnehåll och reklamrelaterat innehåll i en HLS-video-on-demand-ström (VOD). Inspelningsprocessen håller inte reda på de annonsrelaterade segmenten, så informationen som är relaterad till annonsernas placering i huvudinnehållet går förlorad.

Ni kan kanske få den information som är relaterad till positioneringen av annonsinnehållsperioderna från andra källor utanför bandet, som externa CMS-system. Du kan definiera anpassade markörer, genom vilka den här out-of-band-informationen kan skickas till undersystemet för tidslinjehantering. Avsikten är att markera de avsnitt av innehållet som matchar det angivna annonsrelaterade innehållet på ett sådant sätt att alla annonsspecifika uppspelningshändelser utlöses på samma sätt som om dessa anpassade annonsperioder uttryckligen placerades på spelarens tidslinje.

Annonsuppföljning hanteras inte internt av TVSDK, t.ex. när annonser löses av Adobe Primetimes annonsbeslut (tidigare Auditude). TVSDK innehåller dock följande abstraktioner som definierar hur annonsrelaterat innehåll visas på tidslinjen:

* Annonsbrytning

   En annonsbrytning är en ordnad lista med enskilda annonser i följd.
* En enskild annons

Uppspelningshändelser utlöses separat för annonsbrytningar och annonser vid start- och slutpunkten för varje annons.

TVSDK skickar annonsuppföljningshändelser till ditt program, så att du kan implementera din egen spårningslogik. Om du ställer in anpassade annonsmarkörer får du händelserna `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete`och `onAdBreakComplete` .
