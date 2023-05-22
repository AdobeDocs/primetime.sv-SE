---
description: Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.
title: Definiera reservannonsbeteenden för VMAP-textbundna annonser
exl-id: 50de85b0-df2b-422f-893c-dfa641b4901e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Definiera reservannonsbeteenden för VMAP-textbundna annonser {#define-fallback-ad-behavior-for-vmap-inline-ads}

Du kan aktivera reserv när en intern VMAP-fil innehåller en ogiltig medietyp.

1. Ange `setFallbackOnInvalidCreativeEnabled` till `true` för att få VMAP tillbaka när medietypen för en linjär/intern annons är ogiltig för HLS.

   Standardvärdet är `false`. Om en linjär annons misslyckas på grund av att den har en ogiltig medietyp, eller eftersom annonsen inte kan paketeras om, tillåter den här flaggan Primetime-annonsbeslut att följa samma reservbeteende som om annonsen var en tom VAST-wrapper.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
