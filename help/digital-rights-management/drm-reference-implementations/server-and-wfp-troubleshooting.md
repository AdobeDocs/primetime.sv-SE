---
title: Felsökning
description: Felsökning
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Felsökning{#troubleshooting}

Nedan följer några problem och lösningar som du kan stöta på under distributionen.

* Om följande felmeddelande visas:

   ```
   "Error decoding the password for HandlerConfiguration.ServerTransportCredential.password  
       javax.crypto.IllegalBlockSizeException: Input length must be multiple of 8 when decrypting with padded cipher"
   ```

   Kontrollera att lösenordet har krypterats med klassen `ScrambleUtil`.

* Om följande felmeddelande visas:

   ```
   "Unable to load credential from file.pfx -- possibly wrong password."
   ```

   Kontrollera att du har angett rätt krypterat lösenord i PFX-filen.

* Om följande felmeddelande visas:

   ```
   "javax.crypto.BadPaddingException: Given final block not properly padded"
   ```

   Kontrollera att du använder lösenordsspårarklassen *som ingår i referensimplementeringen*. Det här kraschverktyget skiljer sig från det som ingår i Adobe Primetime DRM Server for Protected Streaming.

