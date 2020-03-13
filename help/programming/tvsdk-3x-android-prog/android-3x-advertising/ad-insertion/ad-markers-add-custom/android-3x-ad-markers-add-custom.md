---
description: Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.
seo-description: Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.
seo-title: Lägga till egna annonsmärken
title: Lägga till egna annonsmärken
uuid: 47b08d5e-8d99-4048-a579-77804a5edcdd
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Översikt {#add-custom-ad-markers-overview}

Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.

Den här funktionen är mest användbar när innehåll spelas in, till exempel från en live-händelse, och resultatet av inspelningen är en HLS-ström. Inspelningen innehåller huvudinnehållet och reklamrelaterat innehåll i en HLS-video-on-demand-ström (VOD). Inspelningsprocessen håller inte reda på de annonsrelaterade segmenten, så informationen som är relaterad till annonsernas placering i huvudinnehållet går förlorad.

Ni kan kanske få den information som är relaterad till positioneringen av annonsinnehållsperioderna från andra källor utanför bandet, som externa CMS-system. Du kan definiera anpassade markörer, genom vilka den här out-of-band-informationen kan skickas till undersystemet för tidslinjehantering. Avsikten är att markera de avsnitt av innehållet som matchar det angivna annonsrelaterade innehållet på ett sådant sätt att alla annonsspecifika uppspelningshändelser utlöses på samma sätt som om dessa anpassade annonsperioder uttryckligen placerades på spelarens tidslinje.

Annonsuppföljning hanteras inte internt av TVSDK, till exempel när annonser löses av Adobe Primetimes annonsbeslut. TVSDK innehåller dock följande abstraktioner som definierar hur annonsrelaterat innehåll visas på tidslinjen:

* Annonsbrytning

   En annonsbrytning är en ordnad lista med enskilda annonser i följd.
* En enskild annons

Uppspelningshändelser utlöses separat för annonsbrytningar och annonser vid start- och slutpunkten för varje annons.

TVSDK skickar annonsuppföljningshändelser till ditt program, så att du kan implementera din egen spårningslogik. Om du ställer in anpassade annonsmarkörer får du händelserna `onAdBreakStart`, `onAdStart`, `onAdProgress`, `onAdComplete`och `onAdBreakComplete` .