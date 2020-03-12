---
seo-title: Översikt över begärandecertifikat
title: Översikt över begärandecertifikat
uuid: 3a4e79d7-1832-49d8-bcf2-a029b3729e6d
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# Översikt {#request-certificates-overview}

Om du vill använda Adobe Primetime DRM Production SDK upprepar du följande steg för att begära varje certifikat (License Server, Packager och Transport). SDK:t för utvärdering och SDK:n för testversioner använder ett enda certifikat.

>[!NOTE]
>
>Exemplen i det här dokumentet använder OpenSSL. Du kan även använda andra verktyg. Använd dessa exempel endast som referens. Mer information om hur du genererar nyckelpar och lagrar nycklar och certifikat i HSM-modulen (Hardware Security Module) finns i dokumentationen för HSM-modulen.