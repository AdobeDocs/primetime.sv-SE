---
description: Med lösenordsmodulen krypteras ett lösenord för Adobe Primetime DRM-servern för konfigurationsfiler för skyddad direktuppspelning.
title: Lösenordsskrubbare
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

Alla lösenord som du har angett i filerna [!DNL flashaccess-global.xml] och [!DNL flashaccess-tenant.xml] måste krypteras.

>[!NOTE]
>
>Verktyget Password Scrambler i Primetime DRM-servern för skyddad direktuppspelning är inte utbytbart med den skriptare som finns i Reference Implementation License Server.