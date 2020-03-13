---
seo-title: Hämta certifikat för domän-certifikatutfärdare
title: Hämta certifikat för domän-certifikatutfärdare
uuid: 41bbe02b-363a-47f4-9cc0-350730b6c787
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# Hämta certifikat för domän-certifikatutfärdare{#obtain-domain-ca-certificates}

Till skillnad från licensservern, Packager eller Transportcertifikatet utfärdas inte domänkontrollantcertifikatet av Adobe. Du kan hämta det här certifikatet från en certifikatutfärdare, eller så kan du generera ett självsignerat certifikat som kan användas för detta ändamål.

Domäncertifikatutfärdarcertifikatet bör använda en 1024-bitarsnyckel och innehålla de standardattribut som krävs i ett certifikatutfärdarcertifikat:

* Tillägget Grundläggande begränsningar med CA-flaggan inställd på true
* Tillägget för nyckelanvändning som anger certifikatsignering är tillåtet

Med OpenSSL kan till exempel ett självsignerat certifikatutfärdarcertifikat genereras på följande sätt:

1. Skapa en fil med namnet [!DNL ca-extensions.txt] :

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. Generera nyckel:

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. Generera CSR:

   ```
   openssl req -new -key domain-ca.key -out domain-ca.csr 
   ```

1. Generera certifikat:

   ```
   openssl x509 -req -days 365 -in domain-ca.csr -signkey domain-ca.key \ 
     -out domain-ca.cer -extfile ca-extensions.txt 
   ```

1. Generera lösenord:

   ```
   openssl rand -base64 8 
   ```

1. Generera PFX:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```

