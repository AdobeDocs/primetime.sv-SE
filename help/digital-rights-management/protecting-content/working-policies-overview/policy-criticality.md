---
seo-title: Kritisk DRM-policy
title: Kritisk DRM-policy
uuid: ddc03142-7acb-4a9f-a367-e34cfc5e78ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Kritisk DRM-policy{#drm-policy-criticality}

Om du planerar att tillämpa nya användningsregler i en DRM-princip, och om du tänker använda den här DRM-principen i innehåll som har paketerats för äldre licensservrar (och därför inte tolkar de nya användningsreglerna korrekt), kan du behöva ange hur äldre licensservrar ska bete sig. Som standard anges DRM-principens kritikalitet till `true`.

Den här inställningen anger att licensservern måste bearbeta alla delar av DRM-principen innan den kan generera en licens som använder den angivna DRM-principen. Om DRM-principens kritikalitet är inställd på `false`kan en äldre licensserver ignorera de delar av DRM-principen som den inte kan tolka korrekt. Det innebär att alla licenser som genereras av servern inte innehåller några nya användningsregler.

Primetime DRM-servrar som stöder version 2.0.2 av SDK eller senare accepterar inställningen för DRM-principens kritikalitet.
