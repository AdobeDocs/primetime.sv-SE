---
description: Referensimplementeringen visar hur du ställer in spelaren för annonser, vilket innefattar att ställa in videometadata för annonsinfogning och matcha pre-, mid- och post-roll-annonser i VOD- eller live/linear video streams. Det visar också hur man hanterar klickbara annonser.
title: Annonsinfogning
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
