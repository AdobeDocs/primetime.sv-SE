---
description: Följande krypteringsalternativ väljs vid paketering och kan inte ändras under licensköp.
title: Nyckelrotation
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Nyckelrotation{#key-rotation}

Följande krypteringsalternativ väljs vid paketering och kan inte ändras under licensköp.

Under paketeringen krypteras innehållet vanligtvis med ColdFusion Key (CEK) och klienten får en licens som innehåller CK för att kunna använda innehållet. När tangentrotation är aktiverat används rotationsnyckeln för att kryptera innehållet och nyckeln kan ändras så att varje rotationsnyckel bara används för att kryptera en del av innehållet. Rotationsnycklarna skyddas med hjälp av innehållskrypteringsnyckeln och klienten får fortfarande en licens som innehåller CEK-värdet för att kunna använda innehållet. Paketeringsimplementeringen kan styra vilken innehållskrypteringsnyckel och vilka rotationsnycklar som används samt hur ofta rotationsnycklarna ändras.

Innehåll som paketerats med tangentrotation kan bara spelas upp på Adobe Access-klienter version 3.0 eller senare. Äldre kunder måste uppgradera för att kunna spela upp det här innehållet.
