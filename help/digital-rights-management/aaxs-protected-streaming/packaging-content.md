---
title: Paketera innehåll
description: Paketera innehåll
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Paketerar innehåll{#packaging-content}

Vid paketering av innehåll måste licensserverns URL anges. Adobe Access Server URL har följande format:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

För licensserverns värdnamn &quot;mylicensserver.com&quot; som lyssnar på port 8080 och en klientorganisation som heter &quot;tenant1&quot; är licensserverns URL som anger vid paketeringen:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Om varje innehavare använder en annan licensserver och transportautentiseringsuppgifter måste du ange rätt innehavarcertifikat i paketeraren.

För att säkerställa att servern endast utfärdar licenser till innehåll som paketeras av kända paketerare, inkluderar du paketerarens certifikat i paketerarens tillåtelselista i klientkonfigurationsfilen.
