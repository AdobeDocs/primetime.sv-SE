---
title: Global konfigurationsfil
description: Global konfigurationsfil
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Global konfigurationsfil{#global-configuration-file}

Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern. Filen måste finnas i *LicenseServer.ConfigRoot*. Se katalogen configs för ett exempel på en global konfigurationsfil. Den globala konfigurationsfilen innehåller följande:

* Cachelagring - Styr cachelagring av konfigurationsfiler i minnet. En förklaring av cachelagringsinställningarna finns i&quot;Uppdatera konfigurationsfiler&quot;.
* Loggning - Anger loggningsnivån och hur ofta loggfiler rullas.
* HSM-lösenord - Krävs endast om en HSM används för att lagra serverautentiseringsuppgifter.

Mer information finns i kommentarerna i den globala konfigurationsfilen som finns i `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs`.
