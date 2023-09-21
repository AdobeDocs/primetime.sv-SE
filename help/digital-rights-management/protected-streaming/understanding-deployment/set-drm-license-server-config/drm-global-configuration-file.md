---
description: Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern.
title: Global konfigurationsfil
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Global konfigurationsfil{#global-configuration-file}

Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern.

Du måste placera konfigurationsfilen i [!DNL LicenseServer.ConfigRoot] katalog.

Se [!DNL configs] katalog för ett exempel på en global konfigurationsfil.

Den globala konfigurationsfilen innehåller:

* Cachelagring - Styr cachelagring av konfigurationsfiler i minnet.

  Se *Konfigurationsfiler uppdateras* för information om cachelagringsinställningarna.
* Loggning - Anger loggningsnivån och hur ofta loggfiler rullas.
* HSM-lösenord - Krävs endast om en HSM används för att lagra serverautentiseringsuppgifter.

Se kommentarerna i den globala konfigurationsfilen som finns i Primetime DRM `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs för mer information.
