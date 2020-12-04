---
description: 'null'
seo-description: 'null'
seo-title: Felsökning
title: Felsökning
uuid: 06b86067-1ff6-4b4e-922f-7f968260ba19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
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

