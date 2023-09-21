---
title: Asymmetrisk nyckelkryptering
description: Asymmetrisk nyckelkryptering
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Asymmetrisk nyckelkryptering{#asymmetric-key-encryption}

Asymmetrisk nyckelkryptering (kallas även kryptering med offentlig nyckel) använder nyckelpar. Den ena nyckeln används för kryptering och den andra för dekryptering. Dekrypteringsnyckeln hålls hemlig och kallas *privat nyckel*. Krypteringsnyckeln, som kallas *publik nyckel*, är tillgängligt för alla som har behörighet att kryptera innehåll. Alla som har tillgång till den offentliga nyckeln kan kryptera innehållet, men bara den som har åtkomst till den privata nyckeln kan dekryptera innehållet. Den privata nyckeln kan inte rekonstrueras från den offentliga nyckeln.

När du paketerar innehåll används licensserverns offentliga nyckel för att kryptera innehållskrypteringsnyckeln (CEK) i DRM-metadata. Du måste se till att bara licensservern har tillgång till licensserverns privata nyckel. Om någon annan har nyckeln kan de dekryptera och visa innehållet.

***Varning:**Kontrollera att du har fått licensserverns certifikat (som innehåller den offentliga nyckeln) från en betrodd källa så att du kan vara säker på att det är licensserverns nyckel, och inte en offentlig icke-konfidentiell nyckel. Om en angripare skulle ersätta sin offentliga nyckel för licensserverns nyckel skulle de kunna dekryptera innehållet.*

Mer information om paketeringsinnehåll finns i *Använda Adobe Access SDK för att skydda innehåll*.
