---
description: Konfigurationsfilen flashaccess-global.xml innehåller inställningar som gäller för alla innehavare av licensservern.
title: Global konfigurationsfil
exl-id: 3e74bce6-1634-469f-9d02-1121e9d50687
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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

   Se *Konfigurationsfiler uppdateras* om du vill ha information om cachelagringsinställningarna.
* Loggning - Anger loggningsnivån och hur ofta loggfiler rullas.
* HSM-lösenord - Krävs endast om en HSM används för att lagra serverautentiseringsuppgifter.

Se kommentarerna i den globala konfigurationsfilen som finns i Primetime DRM `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs för mer information.
