---
description: Om du väljer en HSM för att lagra serverinloggningsuppgifterna måste du läsa in privata nycklar och certifikat till HSM och skapa en pkcs11.cfg-konfigurationsfil.
seo-description: Om du väljer en HSM för att lagra serverinloggningsuppgifterna måste du läsa in privata nycklar och certifikat till HSM och skapa en pkcs11.cfg-konfigurationsfil.
seo-title: HSM-konfiguration
title: HSM-konfiguration
uuid: 3610840b-082e-4a73-8aa5-5065f9232e0b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# HSM-konfiguration{#hsm-configuration}

Om du väljer en HSM för att lagra serverinloggningsuppgifterna måste du läsa in privata nycklar och certifikat till HSM och skapa en pkcs11.cfg-konfigurationsfil.

Du måste hitta konfigurationsfilen i katalogen *LicenseServer.ConfigRoot*.

Se katalogen [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] på dvd-skivan för Adobe Primetime DRM för ett exempel på PKCS11-konfigurationsfil.

Se dokumentationen till Sun PKCS11-providern om formatet för [!DNL pkcs11.cfg]-filen.

Du kan använda följande kommando från katalogen där [!DNL pkcs11.cfg]-filen finns ( [!DNL keytool] är installerad med Java JRE och JDK) för att verifiera att konfigurationsfilen för HSM och Sun PKCS1 har konfigurerats korrekt:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Om du kan visa dina inloggningsuppgifter i listan är HSM korrekt konfigurerat och licensservern kan nu komma åt inloggningsuppgifterna.
