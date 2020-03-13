---
seo-title: Paketera innehåll
title: Paketera innehåll
uuid: 366c8470-b7ef-4a39-83c2-151ba9be9a32
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c

---


# Paketera innehåll{#packaging-content}

När du paketerar innehåll för leverans av fjärrnycklar ska du använda en profil som anger att leverans av fjärrnycklar krävs. Nyckelserverns URL måste inkluderas i M3U8 (manifestfil) för HLS-innehållet. Primetimes DRM Key Server-URL har följande format:

```
https://key-server-host:port/faxsks/tenant-name/key
```

För nyckelserverns värdnamn som avlyssnar port 443 och en klientorganisation [!DNL mykeyserver.com] `tenant1`är nyckelserverns URL som ska anges i M3U8:

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

Samma URL kan användas för både iOS- och Xbox 360-klienter. Om servern är konfigurerad med separata klientorganisationer för varje klienttyp kan olika URL:er användas.

Samma innehåll kan spelas upp på klienter som inte behöver en nyckelserver, förutsatt att licensserverns URL pekar på en korrekt konfigurerad licensserver som körs.
