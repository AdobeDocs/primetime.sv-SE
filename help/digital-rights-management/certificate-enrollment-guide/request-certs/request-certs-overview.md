---
title: Översikt över begärandecertifikat
description: Översikt över begärandecertifikat
copied-description: true
exl-id: 4ecdc3be-7db3-494c-af9e-fd4d57b988e4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Översikt {#request-certificates-overview}

Om du vill använda Adobe Primetime DRM Production SDK upprepar du följande steg för att begära varje certifikat (licensserver, Packager och Transport). SDK:t för utvärdering och SDK:n för testversioner använder ett enda certifikat.

>[!NOTE]
>
>Exemplen i det här dokumentet använder OpenSSL. Du kan även använda andra verktyg. Använd dessa exempel endast som referens. Mer information om hur du genererar nyckelpar och lagrar nycklar och certifikat i HSM-modulen (Hardware Security Module) finns i dokumentationen för HSM-modulen.
