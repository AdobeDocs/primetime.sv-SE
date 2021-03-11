---
description: När du paketerar innehåll måste du ange licensserverns URL.
title: Paketera innehåll
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Paketerar innehåll{#packaging-content}

När du paketerar innehåll måste du ange licensserverns URL.

Adobe Primetime DRM Server-URL har följande format:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

För licensserverns värdnamn `mylicenseserver.com` som avlyssnar port 8080 och en klientorganisation som heter *`tenant1`* använder du följande syntax för licensserverns URL som du anger när du paketerar innehåll:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Om varje innehavare använder en annan licensserver och transportautentiseringsuppgifter måste du ange rätt innehavarcertifikat i paketeraren.

Om du vill vara säker på att servern bara utfärdar licenser till innehåll från kända paketerare måste du inkludera paketerarens certifikat i paketeraren tillåtelselista i klientkonfigurationsfilen.
