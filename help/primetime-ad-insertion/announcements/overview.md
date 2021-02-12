---
title: Adobe Primetime Ad Insertion
seo-title: Adobe Primetime Ad Insertion
description: Kommentarer om de senaste funktionsreleaserna och andra relaterade nyheter om Primetime Ad Insertion
seo-description: Kommentarer om de senaste funktionsreleaserna och andra relaterade nyheter om Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Primetime Ad Insertion Announcements

## Minska programmatiska annonseringsfel via tidsgränser för annonsupplösning

Publicerad 1 december 2000

Adobe fokuserar på att hjälpa våra Primetime Ad Insertion-kunder att maximera avkastningen på sitt annonslager. Vi är särskilt uppmärksamma på att minska komplexiteten med att uppfylla programmatiska krav, som enligt eMarketer står för över tre fjärdedelar av USA:s utgifter för digital video och annonsering. Programmatisk försäljning ger utgivaren möjlighet att maximera efterfrågan på sitt annonslager, vilket leder till högre fyllnadsgrad och avkastning. Men det ökar också exponeringen för annonsfel som felaktiga VAST-svar, HTTP-fel och andra som kan leda till förlorade intäkter och/eller dåliga tittarupplevelser.

Ett vanligt problem är långsamma annonssvar från programmatiska partner. Programatiska annonstransaktioner inträffar vanligtvis i millisekunder. Ibland kan det dock ta lång tid för en enda förbrukningskälla att svara. En fördröjning från en enskild leverantör kan påverka hela annonsprocessen, vilket kan orsaka tillfälliga tomma skärmar för användaren, ofyllda annonsplatser eller, i extrema fall, behovet av att starta om en videoström. Tyvärr är det en stor utmaning att identifiera och kringgå långsamma efterfrågningskällor.

För att åtgärda detta problem har Adobe lagt till nya verktyg i Primetime Ad Insertion som gör att kunderna kan ange tidsbegränsningar för annonsupplösning. Om du ställer in dessa regler kringgås källor med långsam efterfrågan automatiskt, vilket säkerställer att videospelarna får annonssvar i tid. På så sätt kan utgivare avsevärt begränsa avbrott från långsamma efterfrågningskällor, vilket hjälper dem att maximera lagerfyllnadstakten och leverera tittarupplevelser i tevekvalitet utan avbrott.

Om du vill aktivera timeout för annonsupplösning i Primetime Ad Insertion ändrar du dina bootstrap-API:er så att den inkluderar ptadtimeout-parametern (längd i millisekunder).  Annonsförfrågningar som inte slutförs innan tidsgränsen uppnås sammanfogas inte (eventuella reservannonser bearbetas).