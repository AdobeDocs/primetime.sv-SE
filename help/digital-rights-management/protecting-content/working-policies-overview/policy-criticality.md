---
title: Kritisk DRM-policy
description: Kritisk DRM-policy
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Kritisk DRM-policy{#drm-policy-criticality}

Om du planerar att tillämpa nya användningsregler i en DRM-princip, och om du tänker använda den här DRM-principen i innehåll som har paketerats för äldre licensservrar (och därför inte tolkar de nya användningsreglerna korrekt), kan du behöva ange hur äldre licensservrar ska bete sig. DRM-principens kritikalitet är som standard inställd på `true`.

Den här inställningen anger att licensservern måste bearbeta alla delar av DRM-principen innan den kan generera en licens som använder den angivna DRM-principen. Om DRM-principens kritikalitet är inställd på `false`kan en äldre licensserver ignorera de delar av DRM-principen som inte kan tolkas korrekt. Det innebär att alla licenser som genereras av servern inte innehåller några nya användningsregler.

Primetime DRM-servrar som stöder version 2.0.2 av SDK eller senare accepterar inställningen för DRM-principens kritikalitet.
