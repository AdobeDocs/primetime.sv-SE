---
title: Asymmetrisk nyckelkryptering
description: Asymmetrisk nyckelkryptering
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Asymmetrisk nyckelkryptering{#asymmetric-key-encryption}

Asymmetrisk nyckelkryptering (kallas även kryptering med offentlig nyckel) använder nyckelpar. En nyckel används för kryptering. den andra för dekryptering. Dekrypteringsnyckeln hålls hemlig och kallas *privat nyckel*. Krypteringsnyckeln, som kallas *offentlig nyckel*, är tillgänglig för alla som har behörighet att kryptera innehåll. Alla som har tillgång till den offentliga nyckeln kan kryptera innehållet, men bara den som har åtkomst till den privata nyckeln kan dekryptera innehållet. Den privata nyckeln kan inte rekonstrueras från den offentliga nyckeln.

När du paketerar innehåll används licensserverns offentliga nyckel för att kryptera innehållskrypteringsnyckeln (CEK) i DRM-metadata. Du måste se till att bara licensservern har tillgång till licensserverns privata nyckel; om någon annan har nyckeln kan de dekryptera och visa innehållet.

***Varning:**Se till att du hämtar licensserverns certifikat (som innehåller den offentliga nyckeln) från en betrodd källa så att du kan vara säker på att det är licensserverns nyckel och inte en offentlig rogue-nyckel. Om en angripare skulle ersätta sin offentliga nyckel för licensserverns nyckel, skulle de kunna dekryptera ditt innehåll.*

Mer information om att paketera innehåll finns i *Använda Adobe Access SDK för att skydda innehåll*.
