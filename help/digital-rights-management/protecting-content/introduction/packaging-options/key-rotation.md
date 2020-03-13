---
description: 'Du kan välja följande krypteringsalternativ när du skapar ett paket. Du kan dock inte ändra krypteringsalternativen när du skaffar licenser '
seo-description: 'Du kan välja följande krypteringsalternativ när du skapar ett paket. Du kan dock inte ändra krypteringsalternativen när du skaffar licenser '
seo-title: Nyckelrotation
title: Nyckelrotation
uuid: 6ac3b828-2cd1-42df-b9ee-4daa8e553d5e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Nyckelrotation {#key-rotation}

Du kan välja följande krypteringsalternativ när du skapar ett paket. Du kan dock inte ändra krypteringsalternativen när du skaffar licenser:

Under paketeringen krypteras innehåll vanligtvis med ColdFusion Key (CEK). Klienten får en licens som innehåller CEK för att förbruka innehållet.

När du aktiverar tangentrotation används rotationsnyckeln för att kryptera innehållet, och nyckeln kan ändras så att varje rotationsnyckel bara används för att kryptera en del av innehållet. Rotationsnycklarna skyddas med hjälp av innehållskrypteringsnyckeln och klienten får fortfarande en licens som innehåller CEK-värdet för att använda innehållet.

Paketeringsimplementeringen kan styra vilken innehållskrypteringsnyckel och vilka rotationsnycklar som används samt hur ofta rotationsnycklarna ändras.

>[!NOTE]
>
>Innehåll som paketerats med nyckelrotation kan bara spelas upp på Primetime DRM-klienter version 3.0 eller senare. Äldre kunder kan behöva uppgradera för att kunna spela upp det här innehållet.