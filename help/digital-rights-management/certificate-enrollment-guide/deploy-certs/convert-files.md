---
title: Konvertera filer
description: Konvertera filer
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Konvertera filer{#convert-files}

Med hjälp av ett verktyg som OpenSSL och den privata nyckeln skapar den begärande filen filerna PKCS#12 (pfx) och PEM/DER genom att ange följande kommandon från ett kommandofönster:

1. Konvertera PKCS#7-filen till en tillfällig PEM-fil.

   Om du vill använda OpenSSL öppnar du ett kommandofönster och anger följande:

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >Denna tillfälliga PEM innehåller ditt certifikat och certifikaten för mellanliggande certifikatutfärdare. Använd dessa certifikat för att generera PFX-filen.

1. Konvertera den tillfälliga PEM-filen till en PFX-fil.

   Om du vill använda OpenSSL öppnar du ett kommandofönster och anger följande:

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. Konvertera den tillfälliga PEM-filen till en slutgiltig PEM-fil.

   Om du vill använda OpenSSL öppnar du ett kommandofönster och anger följande:

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >Även om det inte är obligatoriskt rekommenderar Adobe att du använder olika lösenord för den privata nyckeln (private_key_password) och PFX (pfx_password).

   Den här slutliga PEM-filen innehåller bara ditt certifikat.

1. Konvertera PEM-filen till en DER-fil.

   Om du vill använda OpenSSL öppnar du ett kommandofönster och anger följande:

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >DER-filer krävs bara för HTTP Dynamic Streaming-paketeraren.

