---
title: Kritisk DRM-policy
description: Kritisk DRM-policy
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Kritisk DRM-princip{#drm-policy-criticality}

Om du planerar att tillämpa nya användningsregler i en DRM-princip, och om du tänker använda den här DRM-principen i innehåll som har paketerats för äldre licensservrar (och därför inte tolkar de nya användningsreglerna korrekt), kan du behöva ange hur äldre licensservrar ska bete sig. DRM-principens kritikalitet är som standard inställd på `true`.

Den här inställningen anger att licensservern måste bearbeta alla delar av DRM-principen innan den kan generera en licens som använder den angivna DRM-principen. Om DRM-principens kritikalitet är inställd på `false` kan en äldre licensserver ignorera de delar av DRM-principen som den inte kan tolka korrekt. Det innebär att alla licenser som genereras av servern inte innehåller några nya användningsregler.

Primetime DRM-servrar som stöder version 2.0.2 av SDK eller senare accepterar inställningen för DRM-principens kritikalitet.
