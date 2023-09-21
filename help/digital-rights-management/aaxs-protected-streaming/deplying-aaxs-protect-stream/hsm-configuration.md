---
title: HSM-konfiguration
description: HSM-konfiguration
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# HSM-konfiguration {#hsm-configuration}

Om du väljer att använda en HSM för att lagra serverinloggningsuppgifterna måste du läsa in de privata nycklarna och certifikaten till HSM och skapa en [!DNL pkcs11.cfg] konfigurationsfil. Den här filen måste finnas i *LicenseServer.ConfigRoot* katalog. Se [!DNL Adobe Access Server for Protected Streaming/configs] på Adobe Access-dvd:n för en exempelkonfigurationsfil för PKCS11. Information om formatet för [!DNL pkcs11.cfg]finns i dokumentationen till Sun PKCS11-providern.

För att verifiera att konfigurationsfilen för HSM och Sun PKCS11 är korrekt konfigurerad kan du använda följande kommando från katalogen där [!DNL pkcs11.cfg] filen finns ( [!DNL keytool] installeras med Java JRE och JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Om du ser dina autentiseringsuppgifter i listan är HSM korrekt konfigurerat och licensservern kan komma åt autentiseringsuppgifterna.

>[!NOTE]
>
>Adobe Access Server for protected Streaming stöder för närvarande inte HSM på 64-bitars Windows OS.
