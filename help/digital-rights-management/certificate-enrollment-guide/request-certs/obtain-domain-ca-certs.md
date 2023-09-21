---
title: Hämta certifikat för domän-certifikatutfärdare
description: Hämta certifikat för domän-certifikatutfärdare
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Hämta certifikat för domän-certifikatutfärdare{#obtain-domain-ca-certificates}

Till skillnad från licensservern, paketeraren eller transportcertifikatet utfärdas inte domänkontrollantcertifikatet av Adobe. Du kan hämta det här certifikatet från en certifikatutfärdare, eller så kan du generera ett självsignerat certifikat som kan användas för detta ändamål.

Domäncertifikatutfärdarcertifikatet bör använda en 1024-bitars nyckel och innehålla de standardattribut som krävs i ett certifikatutfärdarcertifikat:

* Tillägget Grundläggande begränsningar med CA-flaggan inställd på true
* Tillägg för nyckelanvändning som anger certifikatsignering är tillåtet

Med OpenSSL kan till exempel ett självsignerat certifikatutfärdarcertifikat genereras på följande sätt:

1. Skapa en fil med namnet [!DNL ca-extensions.txt] som innehåller

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

1. Generera PDF:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```
