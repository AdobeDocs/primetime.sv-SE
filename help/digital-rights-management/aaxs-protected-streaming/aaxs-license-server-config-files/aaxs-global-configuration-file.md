---
title: Global konfigurationsfil
description: Global konfigurationsfil
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Global konfigurationsfil{#global-configuration-file}

Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern. Den här filen måste finnas i *LicenseServer.ConfigRoot*. Se katalogen configs för ett exempel på en global konfigurationsfil. Den globala konfigurationsfilen innehåller följande:

* Cachelagring - Styr cachelagring av konfigurationsfiler i minnet. En förklaring av cachelagringsinställningarna finns i&quot;Uppdatera konfigurationsfiler&quot;.
* Loggning - Anger loggningsnivån och hur ofta loggfiler rullas.
* HSM-lösenord - Krävs endast om en HSM används för att lagra serverautentiseringsuppgifter.

Se kommentarerna i den globala konfigurationsfilen som finns i `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` för mer information.
