---
title: Paketera innehåll
description: Paketera innehåll
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Paketerar innehåll{#packaging-content}

När du paketerar innehåll för leverans av fjärrnycklar ska du använda en profil som anger att leverans av fjärrnycklar krävs. Nyckelserverns URL måste inkluderas i M3U8 (manifestfil) för HLS-innehållet. Primetimes DRM Key Server-URL har följande format:

```
https://key-server-host:port/faxsks/tenant-name/key
```

För nyckelserverns värdnamn [!DNL mykeyserver.com] som lyssnar på port 443 och en klientorganisation med namnet `tenant1` är nyckelserverns URL som ska anges i M3U8:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

Samma URL kan användas för både iOS- och Xbox 360-klienter. Om servern är konfigurerad med separata klientorganisationer för varje klienttyp kan olika URL:er användas.

Samma innehåll kan spelas upp på klienter som inte behöver en nyckelserver, förutsatt att licensserverns URL pekar på en korrekt konfigurerad licensserver som körs.
