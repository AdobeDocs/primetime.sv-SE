---
description: Verktyget SWF Hash Calculator beräknar sammanfattningen för ett SWF-program som finns i en fil.
title: SWF hash-kalkylator
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---

# SWF hash-kalkylator{#swf-hash-calculator}

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
