---
seo-title: SWF-hash-kalkylator
title: SWF-hash-kalkylator
uuid: c1823208-92d9-47c5-b550-f9cc370b543d
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# SWF-hash-kalkylator{#swf-hash-calculator}

Verktyget SWF Hash Calculator beräknade sammanfattningen för ett SWF-program i en fil. Kör kommandot för att köra hasher:

```
Hasher.bat filename.swf
```

eller kommandot:

```
java -jar libs/flashaccess-hasher.jar filename.swf
```

Verktyget skickar följande meddelande:

```
SWF Hash: hash-of-swf
```

Det här värdet kan användas för att ange SWF-sammanfattningen i [!DNL flashaccess-tenant.xml].
