---
title: SWF Hash Calculator
description: SWF Hash Calculator
copied-description: true
exl-id: 651b31bc-47b5-4388-aa00-27d3bd59da30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
