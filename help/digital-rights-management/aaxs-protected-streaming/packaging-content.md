---
title: Paketera innehåll
description: Paketera innehåll
copied-description: true
exl-id: 85950028-d58d-45b3-9337-9fcabe7cc4c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Paketera innehåll{#packaging-content}

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
