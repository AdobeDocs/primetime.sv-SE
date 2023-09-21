---
description: När du paketerar innehåll måste du ange licensserverns URL.
title: Paketera innehåll
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Paketera innehåll{#packaging-content}

När du paketerar innehåll måste du ange licensserverns URL.

Adobe Primetime DRM Server-URL har följande format:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Exempel: för licensserverns värdnamn `mylicenseserver.com` som lyssnar på port 8080 och en klient som kallas *`tenant1`* använder du följande syntax för licensserverns URL som du anger när du paketerar innehåll:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Om varje innehavare använder en annan licensserver och transportautentiseringsuppgifter måste du ange rätt innehavarcertifikat i paketeraren.

Om du vill vara säker på att servern bara utfärdar licenser till innehåll från kända paketerare måste du inkludera paketerarens certifikat i paketeraren tillåtelselista i klientkonfigurationsfilen.
