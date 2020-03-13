---
seo-title: Asymmetrisk nyckelkryptering
title: Asymmetrisk nyckelkryptering
uuid: 0aae25f1-a609-4c73-9aef-13f8ae63f6e1
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Asymmetrisk nyckelkryptering{#asymmetric-key-encryption}

Asymmetrisk nyckelkryptering (kallas även kryptering med offentlig nyckel) använder nyckelpar. En nyckel används för kryptering. den andra för dekryptering. Dekrypteringsnyckeln hålls hemlig och kallas för en *privat nyckel*. Krypteringsnyckeln, som kallas *offentlig nyckel*, är tillgänglig för alla som har behörighet att kryptera innehåll. Alla som har tillgång till den offentliga nyckeln kan kryptera innehållet, men bara den som har åtkomst till den privata nyckeln kan dekryptera innehållet. Den privata nyckeln kan inte rekonstrueras från den offentliga nyckeln.

När du paketerar innehåll används licensserverns offentliga nyckel för att kryptera innehållskrypteringsnyckeln (CEK) i DRM-metadata. Du måste se till att bara licensservern har tillgång till licensserverns privata nyckel; om någon annan har nyckeln kan de dekryptera och visa innehållet.

***Varning:**Kontrollera att du har fått licensserverns certifikat (som innehåller den offentliga nyckeln) från en betrodd källa så att du kan vara säker på att det är licensserverns nyckel, och inte en offentlig icke-konfidentiell nyckel. Om en angripare skulle ersätta sin offentliga nyckel för licensserverns nyckel skulle de kunna dekryptera innehållet.*

Mer information om att paketera innehåll finns i *Använda Adobe Access SDK för att skydda innehåll*.
