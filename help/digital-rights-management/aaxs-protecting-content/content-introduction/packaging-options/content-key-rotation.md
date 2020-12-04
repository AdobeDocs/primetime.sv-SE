---
description: Följande krypteringsalternativ väljs vid paketering och kan inte ändras under licensköp.
seo-description: Följande krypteringsalternativ väljs vid paketering och kan inte ändras under licensköp.
seo-title: Nyckelrotation
title: Nyckelrotation
uuid: 6ee47c06-9981-4281-b10b-343f8b1e55b7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Nyckelrotation{#key-rotation}

Följande krypteringsalternativ väljs vid paketering och kan inte ändras under licensköp.

Under paketeringen krypteras innehållet vanligtvis med ColdFusion Key (CEK) och klienten får en licens som innehåller CK för att kunna använda innehållet. När tangentrotation är aktiverat används rotationsnyckeln för att kryptera innehållet och nyckeln kan ändras så att varje rotationsnyckel bara används för att kryptera en del av innehållet. Rotationsnycklarna skyddas med hjälp av innehållskrypteringsnyckeln och klienten får fortfarande en licens som innehåller CEK-värdet för att kunna använda innehållet. Paketeringsimplementeringen kan styra vilken innehållskrypteringsnyckel och vilka rotationsnycklar som används samt hur ofta rotationsnycklarna ändras.

Innehåll som paketerats med tangentrotation kan bara spelas upp på Adobe Access-klienter version 3.0 eller senare. Äldre kunder måste uppgradera för att kunna spela upp det här innehållet.
