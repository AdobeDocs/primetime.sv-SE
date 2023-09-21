---
title: Felsökning
description: Felsökning
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

  Kontrollera att lösenordet har krypterats med `ScrambleUtil` klassen.

* Om följande felmeddelande visas:

  ```
  "Unable to load credential from file.pfx -- possibly wrong password."
  ```

  Kontrollera att du har angett rätt krypterat lösenord i PFX-filen.

* Om följande felmeddelande visas:

  ```
  "javax.crypto.BadPaddingException: Given final block not properly padded"
  ```

  Se till att du använder klassen för lösenordsspårning *som ingår i referensimplementeringen*. Det här kraschverktyget skiljer sig från det som ingår i Adobe Primetime DRM Server for Protected Streaming.
