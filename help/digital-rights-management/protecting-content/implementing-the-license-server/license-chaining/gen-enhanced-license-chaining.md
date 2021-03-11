---
title: Förbättrad licenskedja
description: Förbättrad licenskedja
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Förbättrad licenskonedning {#enhanced-license-chaining}

Om en DRM-princip används för att generera en licens som stöder licenssammanlänkning måste servern bestämma om en Leaf-licens, rotlicens eller båda ska utfärdas. Om du vill ta reda på vilken typ av licenssammankoppling som en DRM-princip stöder måste du använda `Policy.getLicenseChainType()` eller anropa `Policy.getRootLicenseId()` för att avgöra om DRM-principen har en rotlicens. Med Adobe Primetime DRM 2.0-licenssammanfogning utfärdar servern vanligtvis en lövlicens första gången en användare begär en licens för en viss dator och därefter en rotlicens. Om du vill avgöra om datorn redan har en bladlicens för den angivna profilen måste du ringa `LicenseRequestMessage.clientHasLeafForPolicy()`.

Med förbättrad kedja av licenser i Adobe Primetime DRM 3.0 rekommenderar vi att man utfärdar både en Leaf och en Root första gången man begär en licens för en viss dator. Om användaren redan har rotlicensen kan servern bara utfärda en löv (ring `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` för att avgöra om klienten redan har en 3.0 Förbättrad rot). För efterföljande licensbegäranden anger klienten sedan att den redan har en löv och en rot, så servern bör utfärda en ny rotlicens. När den förbättrade licenskedjan används måste `setRootKeyRetrievalInfo()` anropas för att ange de autentiseringsuppgifter som krävs för att dekryptera rotkrypteringsnyckeln i DRM-principen.

>[!NOTE]
>
>Om profilen har stöd för 3.0 Förbättrad licenskedning, men klienten är Primetime DRM 2.0, utfärdar servern sedan en 2.0-original som kedjad licens. Använd `LicenseRequestMessage.getClientVersion()` för att fastställa klientversionen.

