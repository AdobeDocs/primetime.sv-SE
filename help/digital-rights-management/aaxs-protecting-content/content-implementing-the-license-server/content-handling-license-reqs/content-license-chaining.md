---
seo-title: Licenskedja
title: Licenskedja
uuid: dcc12663-ef9e-4c73-b837-66fcec39358b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Licenskedja{#license-chaining}

Om policyn som används för att generera licensen stöder licenssammanfogning måste servern bestämma om en Leaf-licens, rotlicens eller båda ska utfärdas. Använd `Policy.getLicenseChainType()` eller ring `Policy.getRootLicenseId()` för att avgöra om principen har en rotlicens om du vill ta reda på vilken typ av licenssammankoppling som en princip stöder. Med Adobe Access 2.0-licenssammanfogning utfärdar servern vanligtvis en lövlicens första gången användaren begär en licens för en viss dator och en rotlicens därefter. Om du vill avgöra om datorn redan har en lövlicens för den angivna principen ringer du `LicenseRequestMessage.clientHasLeafForPolicy()`.
