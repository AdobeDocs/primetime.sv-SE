---
description: För direktsänt/linjärt innehåll ersätter Browser TVSDK ett segment av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.
title: Lösning och infogning av annonser live/linjärt
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Lösning och infogning av annonser live/linjärt{#live-linear-ad-resolving-and-insertion}

För direktsänt/linjärt innehåll ersätter Browser TVSDK ett segment av huvudströmsinnehållet med en annonsbrytning med samma varaktighet, så att tidslinjens varaktighet förblir densamma.

Före och under uppspelning löser Browser TVSDK kända annonser, ersätter delar av huvudinnehållet med annonsbrytningar med samma varaktighet och beräknar om den virtuella tidslinjen om det behövs. Platserna för annonsbrytningarna anges av referenspunkter som definieras av manifestet.

Webbläsarens TVSDK infogar annonser på följande sätt:

* **Före rullning**, som är i början av innehållet.

Webbläsaren TVSDK accepterar annonsbrytningen även om längden är längre eller kortare än referenspunktens ersättningslängd. Som standard har Browser TVSDK stöd för `#EXT-X-CUE` som en giltig annonsmarkör när annonser löses och placeras. Den här markören kräver metadatafältet `DURATION` på några sekunder och referensens unika ID. Till exempel:

```
#EXT-X-CUE:DURATION=27,ID="..."
```

Du kan definiera och abonnera på ytterligare kommandon (taggar).

När uppspelningen har startats uppdaterar videomotorn regelbundet manifestfilen. Webbläsarens TVSDK löser eventuella nya annonser och infogar annonserna när en referenspunkt påträffas i den live- eller linjära ström som definierats i manifestet. När annonserna har lösts och infogats beräknar webbläsaren TVSDK den virtuella tidslinjen igen och skickar en `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` -händelse.

>[!TIP]
>
>För liveströmmar stöder Browser TVSDK endast MP4- och HLS-reklam för pre-roll och middle-roll.
