---
seo-title: Global konfigurationsfil
title: Global konfigurationsfil
uuid: 10370bc0-36ab-4e43-9e75-c46a7177874c
translation-type: tm+mt
source-git-commit: ed1430bdcb590a53fa69b324ef340ad636b2fa7c

---


# Global konfigurationsfil{#global-configuration-file}

Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern. Filen måste finnas i *LicenseServer.ConfigRoot*. Se katalogen configs för ett exempel på en global konfigurationsfil. Den globala konfigurationsfilen innehåller följande:

* Cachelagring - Styr cachelagring av konfigurationsfiler i minnet. En förklaring av cachelagringsinställningarna finns i&quot;Uppdatera konfigurationsfiler&quot;.
* Loggning - Anger loggningsnivån och hur ofta loggfiler rullas.
* HSM-lösenord - Krävs endast om en HSM används för att lagra serverautentiseringsuppgifter.

Mer information finns i kommentarerna i den globala konfigurationsfilen som finns i `<AdobeAccessDVD>\Adobe Access Server for Protected Streaming\configs` .
