---
description: Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.
title: Definiera reservannonser för VMAP-textbundna annonser
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Definiera reservannonser för VMAP-textbundna annonser {#define-fallback-ad-behavior-for-vmap-inline-ads}

Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.

1. Ange `setFallbackOnInvalidCreativeEnabled` till `true` för att få VMAP tillbaka när medietypen för en linjär/intern annons är ogiltig för HLS.

   Standardvärdet är `false`. Om en linjär annons misslyckas på grund av att den har en ogiltig medietyp, eller eftersom annonsen inte kan paketeras om, tillåter den här flaggan Primetime-annonsbeslut att följa samma reservbeteende som om annonsen var en tom VAST-wrapper.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
