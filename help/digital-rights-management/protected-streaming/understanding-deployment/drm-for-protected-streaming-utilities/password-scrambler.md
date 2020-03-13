---
description: Verktyget Password Scrambler krypterar ett lösenord för Adobe Primetime DRM-servern för konfigurationsfiler för skyddad direktuppspelning.
seo-description: Verktyget Password Scrambler krypterar ett lösenord för Adobe Primetime DRM-servern för konfigurationsfiler för skyddad direktuppspelning.
seo-title: Lösenordsskrubbare
title: Lösenordsskrubbare
uuid: 56df0f49-f3fd-464d-b4ba-25e1b497158a
translation-type: tm+mt
source-git-commit: 105dedcfe47a5f454a067e66a95827e638290742

---


# Lösenordsskrubbare {#password-scrambler}

Verktyget Password Scrambler krypterar ett lösenord för Adobe Primetime DRM-servern för konfigurationsfiler för skyddad direktuppspelning.

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

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Verktyget Password Scrambler i Primetime DRM-servern för skyddad direktuppspelning är inte utbytbart med den skriptare som finns i Reference Implementation License Server.