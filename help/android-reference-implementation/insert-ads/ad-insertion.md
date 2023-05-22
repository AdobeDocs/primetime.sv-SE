---
description: Referensimplementeringen visar hur du ställer in spelaren för annonser, vilket innefattar att ställa in videometadata för annonsinfogning och matcha pre-, mid- och post-roll-annonser i VOD- eller live/linear video streams. Det visar också hur man hanterar klickbara annonser.
title: Annonsinfogning
exl-id: 3c2d8fca-2a0e-4577-81f3-7b390f6396e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Annonsinfogning {#ad-insertion}

Referensimplementeringen visar hur du ställer in spelaren för annonser, vilket innefattar att ställa in videometadata för annonsinfogning och matcha pre-, mid- och post-roll-annonser i VOD- eller live/linear video streams. Det visar också hur man hanterar klickbara annonser.

Processen med att konfigurera en spelare för annonsinfogning omfattar:

* **Inmatningsfeed:** Fylla i en inmatning med annonsmetadata. Se [Katalogformat](../set-up-dev-environment/exploring-code/catalog-format.md).
* **Referensimplementeringsadapter:** Tolka indataflödet för att fylla i ett metadataobjekt för annonsering.
* **AdsManager:** Använda AdsManager för att hämta annonsmetadata och skapa motsvarande AdProvider.
