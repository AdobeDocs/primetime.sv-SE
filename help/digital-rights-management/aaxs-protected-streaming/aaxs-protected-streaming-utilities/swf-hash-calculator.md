---
title: SWF-hash-kalkylator
description: SWF-hash-kalkylator
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

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
