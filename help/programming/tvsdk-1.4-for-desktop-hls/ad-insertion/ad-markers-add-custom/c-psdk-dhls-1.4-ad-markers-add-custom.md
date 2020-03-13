---
description: Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.
seo-description: Genom att använda anpassade annonsmarkörer kan du markera specifika avsnitt i huvudinnehållet som reklamrelaterade innehållsperioder.
seo-title: Lägga till egna annonsmärken
title: Lägga till egna annonsmärken
uuid: 7cf76e76-965c-4ee4-a311-e28b5a3b5046
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

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

TVSDK skickar annonsuppföljningshändelser till ditt program, så att du kan implementera din egen spårningslogik. Om du ställer in anpassade annonsmarkörer får du händelserna `AD_BREAK_STARTED`, `AD_STARTED`, `AD_PROGRESS`, `AD_COMPLETED`och `AD_BREAK_COMPLETED` .