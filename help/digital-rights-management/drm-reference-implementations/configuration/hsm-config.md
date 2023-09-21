---
description: Du kan konfigurera referensimplementeringen med Sun PKCS#11-providern som stöder HSM. Även om det inte krävs någon HSM rekommenderas det.
title: HSM-konfiguration
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# HSM-konfiguration{#hsm-configuration}

Du kan konfigurera referensimplementeringen med Sun PKCS#11-providern som stöder HSM. Även om det inte krävs någon HSM rekommenderas det.

Om du vill använda en autentiseringsuppgift på en HSM måste du skapa en konfigurationsfil för Sun PKCS#11-providern. Mer information finns i [Java PCKS#11 Reference Guide](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

Verifiera att konfigurationsfilen för HSM och Sun PKCS#11 har konfigurerats genom att skriva följande kommando med hjälp av nyckelverktyget som installerades med Java JDK:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Du har konfigurerat HSM korrekt om du kan visa dina autentiseringsuppgifter i listan.

>[!NOTE]
>
>Från och med Java 1.7 har 64-bitars Sun Java för Windows inte längre stöd för de PKCS#11-gränssnitt som krävs för att Adobe Primetime DRM ska kunna kommunicera med HSM-enheter. Om du tänker använda ett HSM-kort måste du se till att du använder en 32-bitarsversion av Java eller en JDK som stöder de fullständiga PKCS#11-gränssnitten.
