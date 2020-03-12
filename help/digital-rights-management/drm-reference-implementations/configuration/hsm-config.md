---
description: Du kan konfigurera referensimplementeringen med Sun PKCS#11-providern som stöder HSM. Även om det inte krävs någon HSM rekommenderas det.
seo-description: Du kan konfigurera referensimplementeringen med Sun PKCS#11-providern som stöder HSM. Även om det inte krävs någon HSM rekommenderas det.
seo-title: HSM-konfiguration
title: HSM-konfiguration
uuid: 2741ac40-aa42-4aa7-9864-037f3ed3dee2
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# HSM-konfiguration{#hsm-configuration}

Du kan konfigurera referensimplementeringen med Sun PKCS#11-providern som stöder HSM. Även om det inte krävs någon HSM rekommenderas det.

Om du vill använda en autentiseringsuppgift på en HSM måste du skapa en konfigurationsfil för Sun PKCS#11-providern. Mer information finns i [referenshandboken](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html)för Java PCKS#11.

Verifiera att konfigurationsfilen för HSM och Sun PKCS#11 har konfigurerats genom att skriva följande kommando med hjälp av nyckelverktyget som installerades med Java JDK:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Du har konfigurerat HSM korrekt om du kan visa dina autentiseringsuppgifter i listan.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Från och med Java 1.7 har 64-bitars Sun Java för Windows inte längre stöd för de PKCS#11-gränssnitt som krävs för att Adobe Primetime DRM ska kunna kommunicera med HSM-enheter. Om du tänker använda ett HSM-kort måste du se till att du använder en 32-bitarsversion av Java eller en JDK som har stöd för de fullständiga PKCS#11-gränssnitten.

