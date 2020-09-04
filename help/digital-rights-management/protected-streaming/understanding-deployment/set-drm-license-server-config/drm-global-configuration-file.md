---
description: Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern.
seo-description: Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern.
seo-title: Global konfigurationsfil
title: Global konfigurationsfil
uuid: 294d6cff-be07-4b4b-8aa6-943044a1c56f
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Global konfigurationsfil{#global-configuration-file}

Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern.

Du måste placera konfigurationsfilen i [!DNL LicenseServer.ConfigRoot] katalogen.

Ett exempel på en global konfigurationsfil finns i [!DNL configs] katalogen.

Den globala konfigurationsfilen innehåller:

* Cachelagring - Styr cachelagring av konfigurationsfiler i minnet.

   Mer information om cachelagringsinställningarna finns i *Uppdatera konfigurationsfiler* .
* Loggning - Anger loggningsnivån och hur ofta loggfiler rullas.
* HSM-lösenord - Krävs endast om en HSM används för att lagra serverautentiseringsuppgifter.

Mer information finns i kommentarerna i den globala konfigurationsfilen som finns i Primetime DRM `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs.
