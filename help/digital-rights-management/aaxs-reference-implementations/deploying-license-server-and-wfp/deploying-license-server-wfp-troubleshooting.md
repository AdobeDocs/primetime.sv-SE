---
title: Felsökning
description: Felsökning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Felsökning {#troubleshooting}

Nedan visas vanliga problem och lösningar för distribution:

* Om följande fel visas:

  ```
      "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
      javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
  ```

  Kontrollera att lösenordet är krypterat med den angivna `ScrambleUtil` klassen.

* Om följande fel visas:

  ```
      "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  Kontrollera att du har angett rätt krypterat lösenord för PFX-filen.

* Om följande fel visas:

  ```
      "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  Kontrollera att du har använt den lösenordsspårningsklass som ingår i referensimplementeringen (det här spårningsverktyget skiljer sig från det som finns i Adobe® Access™ Server for Protected Streaming).
