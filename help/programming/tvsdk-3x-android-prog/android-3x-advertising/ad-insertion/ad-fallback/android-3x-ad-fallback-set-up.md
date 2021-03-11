---
description: Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.
title: Definiera reservannonsbeteenden för VMAP-textbundna annonser
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Definiera reservannonsbeteenden för VMAP-textbundna annonser {#define-fallback-ad-behavior-for-vmap-inline-ads}

Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.

1. Ange `setFallbackOnInvalidCreativeEnabled` som `true` om du vill att VMAP ska återställas när medietypen för en linjär/intern annons är ogiltig för HLS.

   Standardvärdet är `false`. Om en linjär annons misslyckas på grund av att den har en ogiltig medietyp, eller eftersom annonsen inte kan paketeras om, tillåter den här flaggan Primetime-annonsbeslut att följa samma reservbeteende som om annonsen var en tom VAST-wrapper.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
