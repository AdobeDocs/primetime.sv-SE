---
title: Översikt över begärandecertifikat
description: Översikt över begärandecertifikat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Översikt {#request-certificates-overview}

Om du vill använda Adobe Primetime DRM Production SDK upprepar du följande steg för att begära varje certifikat (licensserver, Packager och Transport). SDK:t för utvärdering och SDK:n för testversioner använder ett enda certifikat.

>[!NOTE]
>
>Exemplen i det här dokumentet använder OpenSSL. Du kan även använda andra verktyg. Använd dessa exempel endast som referens. Mer information om hur du genererar nyckelpar och lagrar nycklar och certifikat i HSM-modulen (Hardware Security Module) finns i dokumentationen för HSM-modulen.