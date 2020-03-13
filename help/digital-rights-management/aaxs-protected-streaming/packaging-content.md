---
seo-title: Paketera innehåll
title: Paketera innehåll
uuid: 5d1d4b9d-f241-4291-9577-e9de5a8b92be
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# Paketera innehåll{#packaging-content}

Vid paketering av innehåll måste licensserverns URL anges. Adobe Access Server-URL:en har följande format:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

För licensserverns värdnamn &quot;mylicensserver.com&quot; som lyssnar på port 8080 och en klientorganisation som heter &quot;tenant1&quot; är licensserverns URL som anger vid paketeringen:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Om varje innehavare använder en annan licensserver och transportautentiseringsuppgifter måste du ange rätt innehavarcertifikat i paketeraren.

För att säkerställa att servern endast utfärdar licenser till innehåll som paketeras av kända paketerare, inkluderar du paketerarens certifikat i paketerarens vitlista för klientkonfigurationsfilen.
