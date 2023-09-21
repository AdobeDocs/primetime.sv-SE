---
description: Om du väljer en HSM för att lagra serverinloggningsuppgifterna måste du läsa in privata nycklar och certifikat till HSM och skapa en pkcs11.cfg-konfigurationsfil.
title: HSM-konfiguration
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# HSM-konfiguration{#hsm-configuration}

Om du väljer en HSM för att lagra serverinloggningsuppgifterna måste du läsa in privata nycklar och certifikat till HSM och skapa en pkcs11.cfg-konfigurationsfil.

Du måste hitta konfigurationsfilen i *LicenseServer.ConfigRoot* katalog.

Se [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] på Adobe Primetime DRM DVD för en exempelfil för PKCS11-konfiguration.

Se dokumentationen till Sun PKCS11-providern om formatet för [!DNL pkcs11.cfg] -fil.

Du kan använda följande kommando från katalogen där [!DNL pkcs11.cfg] filen finns ( [!DNL keytool] installeras med Java JRE och JDK) för att verifiera att konfigurationsfilen HSM och Sun PKCS1 har konfigurerats korrekt:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Om du kan visa dina autentiseringsuppgifter i listan är HSM korrekt konfigurerat och licensservern kan nu komma åt autentiseringsuppgifterna.
