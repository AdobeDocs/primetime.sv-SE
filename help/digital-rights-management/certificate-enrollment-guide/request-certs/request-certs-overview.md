---
title: Översikt över begärandecertifikat
description: Översikt över begärandecertifikat
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Ökning {#request-certificates-overview}

Om du vill använda Adobe Primetime DRM Production SDK upprepar du följande steg för att begära varje certifikat (licensserver, Packager och Transport). SDK:t för utvärdering och SDK:n för testversioner använder ett enda certifikat.

>[!NOTE]
>
>Exemplen i det här dokumentet använder OpenSSL. Du kan även använda andra verktyg. Använd de här exemplen endast som referens. Mer information om hur du genererar nyckelpar och lagrar nycklar och certifikat i HSM-modulen (Hardware Security Module) finns i dokumentationen för HSM-modulen.
