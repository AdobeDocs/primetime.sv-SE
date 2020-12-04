---
description: Referensimplementeringen visar hur du ställer in spelaren för annonser, vilket innefattar att ställa in videometadata för annonsinfogning och matcha pre-, mid- och post-roll-annonser i VOD- eller live/linear video streams. Det visar också hur man hanterar klickbara annonser.
seo-description: Referensimplementeringen visar hur du ställer in spelaren för annonser, vilket innefattar att ställa in videometadata för annonsinfogning och matcha pre-, mid- och post-roll-annonser i VOD- eller live/linear video streams. Det visar också hur man hanterar klickbara annonser.
seo-title: Annonsinfogning
title: Annonsinfogning
uuid: 75c1d77a-a7ff-4cb6-ad7f-7c83a950b7cb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# Annonsinfogning {#ad-insertion}

Referensimplementeringen visar hur du ställer in spelaren för annonser, vilket innefattar att ställa in videometadata för annonsinfogning och matcha pre-, mid- och post-roll-annonser i VOD- eller live/linear video streams. Det visar också hur man hanterar klickbara annonser.

Processen med att konfigurera en spelare för annonsinfogning omfattar:

* **Inmatningsfeed:** Fylla i en inmatningsfeed med annonsmetadata. Se [Katalogformat](../set-up-dev-environment/exploring-code/catalog-format.md).
* **referensimplementeringsflödeskort:** Tolka indataflödet för att fylla i ett metadataobjekt.
* **AdsManager:** Använda AdsManager för att hämta annonsmetadata och skapa motsvarande AdProvider.