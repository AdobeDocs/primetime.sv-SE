---
seo-title: Förbättrad licenskedja
title: Förbättrad licenskedja
uuid: dc0e0a46-d3cd-44e8-a45d-3e22787be44e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# Förbättrad licenskonedning {#enhanced-license-chaining}

Med förbättrad kedja av licenser i Adobe Access 3.0 rekommenderar vi att man utfärdar både en löv och en rot första gången man begär en licens för en viss dator. Om användaren redan har rotlicensen kan servern bara utfärda en löv (ring `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` för att avgöra om klienten redan har en 3.0 Förbättrad rot). För efterföljande licensbegäranden anger klienten att den redan har en löv och en rot, så servern bör utfärda en ny rotlicens. När den förbättrade licenskedjan används måste `setRootKeyRetrievalInfo()` anropas för att ange de autentiseringsuppgifter som krävs för att dekryptera rotkrypteringsnyckeln i profilen.

>[!NOTE]
>
>Om profilen har stöd för 3.0 Förbättrad licenskedning, men klienten är Adobe Access 2.0, kommer servern att utfärda en 2.0-original som kedjad licens. Använd LicenseRequestMessage.getClientVersion() för att fastställa klientversionen.

