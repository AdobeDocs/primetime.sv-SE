---
seo-title: HSM-konfiguration
title: HSM-konfiguration
uuid: 1cc5be99-c24c-4c1e-9348-fb69f96d8ca5
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# HSM-konfiguration {#hsm-configuration}

Du behöver inte använda HSM, men vi rekommenderar det. Referensimplementeringen kan konfigureras att använda Sun PKCS11-providern för HSM-stöd. För att du ska kunna använda en autentiseringsuppgift på en HSM måste du skapa en konfigurationsfil för Sun PKCS11-providern. Mer information finns i Solens dokumentation. För att verifiera att konfigurationsfilen för HSM och Sun PKCS1 är korrekt konfigurerad kan du använda följande kommando (nyckelverktyget installeras med Java JDK):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Om du ser dina autentiseringsuppgifter i listan är HSM korrekt konfigurerat.

>[!NOTE]
>
>Från och med Java 1.7 har 64-bitars Sun Java för Windows inte stöd för de PKCS11-gränssnitt som krävs för att Adobe Access DRM ska kunna kommunicera med HSM-enheter. Om du tänker använda ett HSM-kort bör du använda en 32-bitarsversion av Java, eller använda en JDK som har stöd för de fullständiga PKCS1-gränssnitten.

