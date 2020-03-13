---
seo-title: HSM-konfiguration
title: HSM-konfiguration
uuid: da4d7118-65a8-460d-a796-b7bf5c28b208
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# HSM-konfiguration {#hsm-configuration}

Om du väljer att använda en HSM för att lagra serverinloggningsuppgifterna måste du läsa in de privata nycklarna och certifikaten till HSM och skapa en [!DNL pkcs11.cfg] konfigurationsfil. Filen måste finnas i katalogen *LicenseServer.ConfigRoot* . Ett exempel på en PKCS1-konfigurationsfil finns i katalogen på dvd-skivan för Adobe Access. [!DNL Adobe Access Server for Protected Streaming/configs] Mer information om formatet för [!DNL pkcs11.cfg]finns i dokumentationen till Sun PKCS11-providern.

För att verifiera att konfigurationsfilen för HSM och Sun PKCS11 är korrekt konfigurerad kan du använda följande kommando från den katalog där [!DNL pkcs11.cfg] filen finns ( [!DNL keytool] installeras med Java JRE och JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Om du ser dina inloggningsuppgifter i listan är HSM korrekt konfigurerat och licensservern kan komma åt inloggningsuppgifterna.

> [!NOTE]
> Adobe Access Server för skyddad direktuppspelning stöder för närvarande inte HSM på 64-bitars Windows.

