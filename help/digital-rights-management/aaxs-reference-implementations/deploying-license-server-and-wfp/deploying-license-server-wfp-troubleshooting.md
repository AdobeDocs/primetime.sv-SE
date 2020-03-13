---
seo-title: Felsökning
title: Felsökning
uuid: db76d6a4-c285-4d86-95a1-4f1a85ed3743
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

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

