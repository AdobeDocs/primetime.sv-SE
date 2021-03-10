---
description: När Primetimes annonsbeslut påträffar en VAST-annons (creative) som är tom eller som har en medietyp som är ogiltig för HLS, utvärderas reservannonserna för att avgöra vad som ska returneras.
title: Annonsbeteende för VAST och VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Annonsbeteende för VAST och VMAP {#ad-fallback-behavior-for-vast-and-vmap}

När Primetimes annonsbeslut påträffar en VAST-annons (creative) som är tom eller som har en medietyp som är ogiltig för HLS, utvärderas reservannonserna för att avgöra vad som ska returneras.

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

I TVSDK är den enda giltiga medietypen `application/x-mpegURL` (M3U8).

När det finns fristående annonser i reserv undersöker Primetime-annonsen dessa annonser i följande ordning och returnerar den första annonsen med en giltig medietyp:

1. Om ompaketering är aktiverat behandlas den första förekomsten av en annons med en ogiltig medietyp som andra ogiltiga medietyper.

   Om ompaketering misslyckas gäller den här processen för ytterligare förekomster av annonsen.
1. Om TVSDK inte hittar några giltiga reservannonser returneras den ursprungliga annonsen med den ogiltiga medietypen.
1. Om en reservannons med en giltig MIME-typ returneras i stället för den ursprungliga annonsen, skickar Primetime ad decisioningfelkod 403 till VAST-fel-URL:en, om en sådan finns.
1. Om en reservannons är en wrapper och returnerar flera annonser returneras bara annonser med rätt medietyp.

>[!IMPORTANT]
>
>Det här beteendet är alltid aktiverat för annonser i VAST-omslutningar. För VAST-annonser som är infogade i en VMAP är beteendet inaktiverat som standard, men programmet kan aktivera det.

