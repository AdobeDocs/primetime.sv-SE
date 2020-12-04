---
seo-title: HSM-konfiguration
title: HSM-konfiguration
uuid: da4d7118-65a8-460d-a796-b7bf5c28b208
translation-type: tm+mt
source-git-commit: ac75f63f98060e1937570476362bb5d4458d1f85
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# HSM-konfiguration {#hsm-configuration}

Om du väljer att använda en HSM för att lagra serverinloggningsuppgifterna måste du läsa in de privata nycklarna och certifikaten till HSM och skapa en [!DNL pkcs11.cfg]-konfigurationsfil. Filen måste finnas i katalogen *LicenseServer.ConfigRoot*. Se katalogen [!DNL Adobe Access Server for Protected Streaming/configs] på dvd-skivan för Adobe Access för ett exempel på en PKCS1-konfigurationsfil. Mer information om formatet för [!DNL pkcs11.cfg] finns i dokumentationen för Sun PKCS11-providern.

För att verifiera att konfigurationsfilen för HSM och Sun PKCS11 är korrekt konfigurerad kan du använda följande kommando från katalogen där [!DNL pkcs11.cfg]-filen finns ( [!DNL keytool] installeras med Java JRE och JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Om du ser dina inloggningsuppgifter i listan är HSM korrekt konfigurerat och licensservern kan komma åt inloggningsuppgifterna.

>[!NOTE]
>
>Adobe Access Server for protected Streaming stöder för närvarande inte HSM på 64-bitars Windows OS.
