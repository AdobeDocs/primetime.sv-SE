---
title: Licenskedja
description: Licenskedja
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Licenskedja{#license-chaining}

Om policyn som används för att generera licensen stöder licenssammanfogning måste servern bestämma om en Leaf-licens, rotlicens eller båda ska utfärdas. Använd `Policy.getLicenseChainType()` eller ring `Policy.getRootLicenseId()` för att avgöra om principen har en rotlicens om du vill ta reda på vilken typ av licenssammankoppling som en princip stöder. Med Adobe Access 2.0-licenssammanfogning utfärdar servern vanligtvis en lövlicens första gången användaren begär en licens för en viss dator och en rotlicens därefter. Om du vill avgöra om datorn redan har en lövlicens för den angivna principen ringer du `LicenseRequestMessage.clientHasLeafForPolicy()`.
