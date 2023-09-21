---
title: Licenskedja
description: Licenskedja
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Licenskedja{#license-chaining}

Om policyn som används för att generera licensen stöder licenssammanfogning måste servern bestämma om en Leaf-licens, rotlicens eller båda ska utfärdas. Om du vill ta reda på vilken typ av licenssammankoppling som en policy stöder använder du `Policy.getLicenseChainType()`eller ringa `Policy.getRootLicenseId()` för att avgöra om profilen har en rotlicens. Med Adobe Access 2.0-licenssammanfogning utfärdar servern vanligtvis en lövlicens första gången användaren begär en licens för en viss dator och en rotlicens därefter. Om du vill avgöra om datorn redan har en lövlicens för den angivna principen ringer du `LicenseRequestMessage.clientHasLeafForPolicy()`.
