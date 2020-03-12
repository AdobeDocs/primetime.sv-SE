---
seo-title: Licenskedja
title: Licenskedja
uuid: dcc12663-ef9e-4c73-b837-66fcec39358b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Licenskedja{#license-chaining}

Om policyn som används för att generera licensen stöder licenssammanfogning måste servern bestämma om en Leaf-licens, rotlicens eller båda ska utfärdas. Om du vill avgöra vilken typ av licenssammanfogning en profil stöder använder `Policy.getLicenseChainType()`eller ringer du `Policy.getRootLicenseId()` för att avgöra om profilen har en rotlicens. Med Adobe Access 2.0-licenssammanfogning utfärdar servern vanligtvis en lövlicens första gången användaren begär en licens för en viss dator och en rotlicens därefter. Om du vill avgöra om datorn redan har en lövlicens för den angivna profilen ringer du `LicenseRequestMessage.clientHasLeafForPolicy()`.
