---
description: Du kan generera uttryckstoken för deras krypterade innehåll genom att skicka tokenbegäranden till rätt Expressplay-tokenserver.
title: Uttryckstoken
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Uttryckstoken {#expressplay-tokens}

Du kan generera uttryckstoken för deras krypterade innehåll genom att skicka tokenbegäranden till rätt Expressplay-tokenserver.

Ett exempel är följande URL:

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

Lagring-ID:t för innehållskrypteringsnyckeln eller CEKSID:t som anges för `kid` -parametern och innehållskrypteringsnyckeln eller CEK som ges till `contentKey` -parametern måste matcha innehållskrypteringsnyckelns lagrings-ID och innehållskrypteringsnyckeln som används för paketering. Följande text är ett exempel på tokenserversvaret:

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

Då kan du antingen

* använda den returnerade URL:en och frågan som licensserverns URL, eller
* ta bort frågan från URL:en och skicka ExpressPlayToken separat som en HTTP-POST
