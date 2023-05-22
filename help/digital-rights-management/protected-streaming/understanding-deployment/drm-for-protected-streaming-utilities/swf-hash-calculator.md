---
description: Verktyget SWF Hash Calculator beräknar sammanfattningen för ett SWF-program som finns i en fil.
title: SWF hash-räknare
exl-id: 245254fe-2fcb-41e8-94bd-0cbc8b39b2b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# SWF hash-räknare{#swf-hash-calculator}

Verktyget SWF Hash Calculator beräknar sammanfattningen för ett SWF-program som finns i en fil.

Om du vill köra hasher skriver du:

```
Hasher.bat 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

eller

```
java -jar libs/flashaccess-hasher.jar 
<i class="+ topic ph hi-d="" i "="">
  filename.swf
</i class="+ topic>
```

Verktyget visar följande meddelande:

```
SWF Hash: 
<i class="+ topic ph hi-d="" i "="">
  hash-of-swf
</i class="+ topic>
```

Du kan använda det här värdet för att ange sammandraget SWF i [!DNL flashaccess-tenant.xml].
