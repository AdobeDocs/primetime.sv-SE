---
seo-title: Lösenordsfasare
title: Lösenordsfasare
uuid: e488babc-cd50-41b9-acb8-490e8e42e8bc
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9
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

