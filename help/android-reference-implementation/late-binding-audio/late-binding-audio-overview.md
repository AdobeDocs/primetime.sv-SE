---
description: Du kan aktivera och bygga kontroller för det sena ljudbindningen.
seo-description: Du kan aktivera och bygga kontroller för det sena ljudbindningen.
seo-title: Översikt
title: Översikt
uuid: 7656f930-f426-426e-bcd4-dfa9d39e7ae4
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Översikt {#overview}

Du kan aktivera och bygga kontroller för det sena ljudbindningen.

HLS-standarden tillåter strömmar i flera format, vilket innebär att vi kan hålla ljud- och videospåren i en ström åtskilda från varandra. Videospåret med flera återgivningar (t.ex. 240p, 480p, 720p och 1080p) och ljudspåren (t.ex. engelska, spanska, franska, tyska) kan kodas separat. Mediespelaren väljer sedan önskade video- och ljudspår och binder dem direkt på klientsidan.

Du kan implementera olika arbetsflöden beroende på vilket användargränssnitt du har. Det allmänna arbetsflödet för Primetime-spelaren är följande:

1. När användaren väljer en video fylls en lista med tillgängliga ljudspår för det medieobjektet i.
1. När användaren trycker på knappen Inställningar i användargränssnittet visas alternativen för ljudspår.
1. När ett ljudspår är markerat blir det aktiva ljudspåret.
1. Slutanvändaren kan trycka på knappen Inställningar för att växla tillbaka till det ursprungliga ljudspåret.

