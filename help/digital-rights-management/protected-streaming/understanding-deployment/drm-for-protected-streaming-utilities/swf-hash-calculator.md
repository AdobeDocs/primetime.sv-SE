---
description: Verktyget SWF Hash Calculator beräknar sammanfattningen för ett SWF-program som finns i en fil.
title: SWF-hash-räknare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---


# SWF-hash-räknare{#swf-hash-calculator}

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

Du kan använda det här värdet för att ange SWF-sammanfattningen i [!DNL flashaccess-tenant.xml].
