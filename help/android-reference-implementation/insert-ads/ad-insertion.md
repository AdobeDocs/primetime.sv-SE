---
description: Referensimplementeringen visar hur du ställer in spelaren för annonser, vilket innefattar att ställa in videometadata för annonsinfogning och matcha pre-, mid- och post-roll-annonser i VOD- eller live/linear video streams. Det visar också hur man hanterar klickbara annonser.
title: Annonsinfogning
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Annonsinfogning {#ad-insertion}

Referensimplementeringen visar hur du ställer in spelaren för annonser, vilket innefattar att ställa in videometadata för annonsinfogning och matcha pre-, mid- och post-roll-annonser i VOD- eller live/linear video streams. Det visar också hur man hanterar klickbara annonser.

Processen med att konfigurera en spelare för annonsinfogning omfattar:

* **Inmatningsfeed:** Fylla i en inmatningsfeed med annonsmetadata. Se [Katalogformat](../set-up-dev-environment/exploring-code/catalog-format.md).
* **referensimplementeringsflödeskort:** Tolka indataflödet för att fylla i ett metadataobjekt.
* **AdsManager:** Använda AdsManager för att hämta annonsmetadata och skapa motsvarande AdProvider.