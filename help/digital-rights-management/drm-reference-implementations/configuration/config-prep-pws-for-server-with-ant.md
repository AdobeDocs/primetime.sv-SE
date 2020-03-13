---
description: 'null'
seo-description: 'null'
seo-title: Förbered lösenord med Ant
title: Förbered lösenord med Ant
uuid: 9419ab0d-b448-4881-9d26-35c00f0b13bc
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Förbered lösenord med Ant{#prepare-passwords-using-ant}

Använd Ant för att kryptera ditt lösenord:

1. Navigera till `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. Ange `sdkdir` egenskapen i [!DNL build-refimpl.xml] för att peka på den katalog som innehåller Primetime DRM Java SDK.
1. Kör följande kommando:

   ```
   ant -f build-refimpl.xml
   ```

