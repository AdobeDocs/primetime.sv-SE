---
description: 'Du kan välja följande krypteringsalternativ när du skapar ett paket. Du kan dock inte ändra krypteringsalternativen när du skaffar licenser '
title: Nyckelrotation
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# Nyckelrotation {#key-rotation}

Du kan välja följande krypteringsalternativ när du skapar ett paket. Du kan dock inte ändra krypteringsalternativen när du skaffar licenser:

Under paketeringen krypteras innehåll vanligtvis med ColdFusion Key (CEK). Klienten får en licens som innehåller CEK för att förbruka innehållet.

När du aktiverar tangentrotation används rotationsnyckeln för att kryptera innehållet, och nyckeln kan ändras så att varje rotationsnyckel bara används för att kryptera en del av innehållet. Rotationsnycklarna skyddas med hjälp av innehållskrypteringsnyckeln och klienten får fortfarande en licens som innehåller CEK-värdet för att använda innehållet.

Paketeringsimplementeringen kan styra vilken innehållskrypteringsnyckel och vilka rotationsnycklar som används samt hur ofta rotationsnycklarna ändras.

>[!NOTE]
>
>Innehåll som paketerats med nyckelrotation kan bara spelas upp på Primetime DRM-klienter version 3.0 eller senare. Äldre kunder kan behöva uppgradera för att kunna spela upp det här innehållet.