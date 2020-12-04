---
description: Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.
seo-description: Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.
seo-title: Definiera reservannonsbeteenden för VMAP-textbundna annonser
title: Definiera reservannonsbeteenden för VMAP-textbundna annonser
uuid: bc8cb0b4-5ea9-429b-ab5d-746c6f03e74b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '130'
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
