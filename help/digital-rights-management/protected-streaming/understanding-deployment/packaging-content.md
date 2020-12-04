---
description: När du paketerar innehåll måste du ange licensserverns URL.
seo-description: När du paketerar innehåll måste du ange licensserverns URL.
seo-title: Paketera innehåll
title: Paketera innehåll
uuid: 2e47a9a2-bbc6-4995-8ce5-6ca6b116349b
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '141'
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
