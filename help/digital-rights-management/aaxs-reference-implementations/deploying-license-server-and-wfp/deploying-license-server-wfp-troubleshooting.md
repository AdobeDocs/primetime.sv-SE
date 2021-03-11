---
title: Felsökning
description: Felsökning
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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

   Kontrollera att lösenordet är krypterat med den angivna klassen `ScrambleUtil`.

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

