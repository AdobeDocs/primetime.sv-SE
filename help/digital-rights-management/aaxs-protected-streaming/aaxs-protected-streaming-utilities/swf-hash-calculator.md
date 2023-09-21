---
title: SWF Hash Calculator
description: SWF Hash Calculator
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---

# SWF Hash Calculator{#swf-hash-calculator}

Verktyget SWF Hash Calculator beräknade sammanfattningen för ett program i SWF som finns i en fil. Kör kommandot för att köra hasher:

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

Det här värdet kan användas för att ange sammandraget SWF i [!DNL flashaccess-tenant.xml].
