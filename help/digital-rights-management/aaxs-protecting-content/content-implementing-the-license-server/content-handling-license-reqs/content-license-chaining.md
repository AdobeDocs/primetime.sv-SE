---
title: Licenskedja
description: Licenskedja
copied-description: true
exl-id: 2f439e21-c748-45aa-a87c-36e70ee3722a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Licenskedja{#license-chaining}

Om policyn som används för att generera licensen stöder licenssammanfogning måste servern bestämma om en Leaf-licens, rotlicens eller båda ska utfärdas. Använd `Policy.getLicenseChainType()`eller ringa `Policy.getRootLicenseId()` för att avgöra om profilen har en rotlicens. Med Adobe Access 2.0-licenssammanfogning utfärdar servern vanligtvis en lövlicens första gången användaren begär en licens för en viss dator och en rotlicens därefter. Om du vill avgöra om datorn redan har en lövlicens för den angivna principen ringer du `LicenseRequestMessage.clientHasLeafForPolicy()`.
