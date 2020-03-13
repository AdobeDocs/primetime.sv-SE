---
description: För direktsänt/linjärt innehåll ersätter Browser TVSDK ett segment av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
seo-description: För direktsänt/linjärt innehåll ersätter Browser TVSDK ett segment av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
seo-title: Lösning och infogning av annonser live/linjärt
title: Lösning och infogning av annonser live/linjärt
uuid: 18c6733a-e827-4b1c-9cd5-796d57cbdb05
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Lösning och infogning av annonser live/linjärt{#live-linear-ad-resolving-and-insertion}

För direktsänt/linjärt innehåll ersätter Browser TVSDK ett segment av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.

Före och under uppspelning löser Browser TVSDK kända annonser, ersätter delar av huvudinnehållet med annonsbrytningar med samma varaktighet och beräknar om den virtuella tidslinjen om det behövs. Platserna för annonsbrytningarna anges av referenspunkter som definieras av manifestet.

Webbläsarens TVSDK infogar annonser på följande sätt:

* **Pre-roll**, som är i början av innehållet.

Webbläsaren TVSDK accepterar annonsbrytningen även om längden är längre eller kortare än referenspunktens ersättningslängd. Som standard har Browser TVSDK stöd för `#EXT-X-CUE` referenspunkten som en giltig annonsmarkör när annonser löses och placeras. Den här markören kräver metadatafältet `DURATION` i sekunder och referensens unika ID. Exempel:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Du kan definiera och abonnera på ytterligare kommandon (taggar).

När uppspelningen har startats uppdaterar videomotorn regelbundet manifestfilen. Webbläsarens TVSDK löser eventuella nya annonser och infogar annonserna när en referenspunkt påträffas i den live- eller linjära ström som definierats i manifestet. När annonserna har lösts och infogats beräknar webbläsaren TVSDK den virtuella tidslinjen igen och skickar en `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` händelse.

>[!TIP]
>
>För liveströmmar stöder Browser TVSDK endast MP4- och HLS-reklam för pre-roll och middle-roll.

