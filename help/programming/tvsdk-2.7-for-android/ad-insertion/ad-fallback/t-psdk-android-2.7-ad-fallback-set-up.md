---
description: Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.
seo-description: Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.
seo-title: Definiera reservannonsbeteenden för VMAP-textbundna annonser
title: Definiera reservannonsbeteenden för VMAP-textbundna annonser
uuid: a7b5c9a6-f546-4d3a-9d49-7e5484acff7a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Definiera reservannonsbeteenden för VMAP-textbundna annonser {#define-fallback-ad-behavior-for-vmap-inline-ads}

Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.

1. Ange `setFallbackOnInvalidCreativeEnabled` att VMAP `true` ska återställas när medietypen för en linjär/textbunden annons är ogiltig för HLS.

   Standardvärdet är `false`. Om en linjär annons misslyckas på grund av att den har en ogiltig medietyp, eller eftersom annonsen inte kan paketeras om, tillåter den här flaggan Primetime-annonsbeslut att följa samma reservbeteende som om annonsen var en tom VAST-wrapper.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

