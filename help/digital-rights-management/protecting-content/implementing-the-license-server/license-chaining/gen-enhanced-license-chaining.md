---
seo-title: Förbättrad licenskedja
title: Förbättrad licenskedja
uuid: f869b4e7-4b24-4832-94a7-b7143567ab58
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Förbättrad licenskedja {#enhanced-license-chaining}

Om en DRM-princip används för att generera en licens som stöder licenssammanlänkning måste servern bestämma om en Leaf-licens, rotlicens eller båda ska utfärdas. Om du vill avgöra vilken typ av licenssammankoppling som en DRM-princip stöder måste du använda `Policy.getLicenseChainType()`eller anropa `Policy.getRootLicenseId()` för att avgöra om DRM-principen har en rotlicens. Med Adobe Primetime DRM 2.0-licenssammanfogning utfärdar servern vanligtvis en bladlicens första gången en användare begär en licens för en viss dator och en rotlicens därefter. Om du vill avgöra om datorn redan har en lövlicens för den angivna profilen måste du ringa `LicenseRequestMessage.clientHasLeafForPolicy()`.

Med förbättrad kedja av licenser i Adobe Primetime DRM 3.0 rekommenderar vi att man utfärdar både en Leaf och en Root första gången man begär en licens för en viss dator. Om användaren redan har rotlicensen kan servern bara utfärda en löv (anropa `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` för att avgöra om klienten redan har en 3.0 Förbättrad rot). För efterföljande licensbegäranden anger klienten sedan att den redan har en löv och en rot, så servern bör utfärda en ny rotlicens. När den förbättrade licenskedjan används måste du anropa den för att ange de inloggningsuppgifter som behövs för att dekryptera rotkrypteringsnyckeln i DRM-principen. `setRootKeyRetrievalInfo()`

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Om profilen har stöd för 3.0 Förbättrad licenskedning, men klienten är Primetime DRM 2.0, utfärdar servern sedan en 2.0-original som kedjad licens. Använd `LicenseRequestMessage.getClientVersion()`för att fastställa klientversionen.

