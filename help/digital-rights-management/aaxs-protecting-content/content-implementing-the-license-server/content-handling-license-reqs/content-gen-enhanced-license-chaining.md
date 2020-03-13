---
seo-title: Förbättrad licenskedja
title: Förbättrad licenskedja
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: da8736769f7b47318dbd955aa854f83ae64d6d7b

---


# Förbättrad licenskedja {#enhanced-license-chaining}

Med förbättrad kedja av licenser i Adobe Access 3.0 rekommenderar vi att man utfärdar både en löv och en rot första gången man begär en licens för en viss dator. Om användaren redan har rotlicensen kan servern bara utfärda en löv (anropa `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` för att avgöra om klienten redan har en 3.0 Förbättrad rot). För efterföljande licensbegäranden anger klienten att den redan har en löv och en rot, så servern bör utfärda en ny rotlicens. När den utökade licenskedjan används måste du anropa `setRootKeyRetrievalInfo()` de autentiseringsuppgifter som behövs för att dekryptera rotkrypteringsnyckeln i profilen.

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Om profilen stöder 3.0 Förbättrad licenskedning, men klienten är Adobe Access 2.0, kommer servern att utfärda en 2.0-original som kedjad licens. Använd LicenseRequestMessage.getClientVersion() för att fastställa klientversionen.

