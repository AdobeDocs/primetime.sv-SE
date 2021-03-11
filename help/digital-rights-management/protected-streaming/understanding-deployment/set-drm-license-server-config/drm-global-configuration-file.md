---
description: Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern.
title: Global konfigurationsfil
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Global konfigurationsfil{#global-configuration-file}

Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern.

Du måste placera konfigurationsfilen i katalogen [!DNL LicenseServer.ConfigRoot].

I katalogen [!DNL configs] finns ett exempel på en global konfigurationsfil.

Den globala konfigurationsfilen innehåller:

* Cachelagring - Styr cachelagring av konfigurationsfiler i minnet.

   Mer information om cachelagringsinställningarna finns i *Uppdatera konfigurationsfiler*.
* Loggning - Anger loggningsnivån och hur ofta loggfiler rullas.
* HSM-lösenord - Krävs endast om en HSM används för att lagra serverautentiseringsuppgifter.

Mer information finns i kommentarerna i den globala konfigurationsfilen som finns i Primetime DRM `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs.
