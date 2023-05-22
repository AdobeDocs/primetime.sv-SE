---
title: Felsökning
description: Felsökning
copied-description: true
exl-id: 4af7b625-63d3-48b6-98a5-b8894dd0c67f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
