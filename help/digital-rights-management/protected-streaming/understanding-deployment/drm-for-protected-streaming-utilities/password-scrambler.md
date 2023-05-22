---
description: Med lösenordsmodulen krypteras ett lösenord för Adobe Primetime DRM-servern för konfigurationsfiler för skyddad direktuppspelning.
title: Lösenordsskrubbare
exl-id: 9cedd3e5-01db-4ea9-bf23-8767987fc26c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# Lösenordsskrubbare {#password-scrambler}

Med lösenordsmodulen krypteras ett lösenord för Adobe Primetime DRM-servern för konfigurationsfiler för skyddad direktuppspelning.

Om du vill köra krysset skriver du:

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

eller

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

Verktyget visar följande meddelande:

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

Alla lösenord som du har angett i [!DNL flashaccess-global.xml] och [!DNL flashaccess-tenant.xml] filer måste krypteras.

>[!NOTE]
>
>Verktyget Password Scrambler i Primetime DRM-servern för skyddad direktuppspelning är inte utbytbart med den skriptare som finns i Reference Implementation License Server.
