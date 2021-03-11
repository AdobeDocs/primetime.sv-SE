---
title: Lösenordsfasare
description: Lösenordsfasare
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---


# Lösenordsschemat {#password-scrambler}

Verktyget Lösenordsspåraren krypterar ett lösenord så att det kan användas i konfigurationsfilerna för skyddad strömning i Adobe Access Server. Kör kommandot för att köra kramaren:

```
Scrambler.bat password 
```

eller kommandot:

```
java -jar libs/flashaccess-scrambler.jar password  
```

Verktyget skickar följande meddelande:

```
Encrypted password: scrambled-password 
```

Alla lösenord som anges i flashaccess-global.xml och flashaccess-tenant.xml måste krypteras.

>[!NOTE]
>
>Verktyget Password Scrambler i Adobe Access Server för skyddad direktuppspelning är inte utbytbart med den skramlare som ingår i Reference Implementation License Server.

