---
title: Global konfigurationsfil
description: Global konfigurationsfil
copied-description: true
exl-id: 5a2f96fe-d39d-4391-a010-200a900b043b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
