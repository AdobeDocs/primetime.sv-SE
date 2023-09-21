---
title: Förbättrad licenskedja
description: Förbättrad licenskedja
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Förbättrad licenskedja {#enhanced-license-chaining}

Med förbättrad kedja av licenser i Adobe Access 3.0 rekommenderar vi att man utfärdar både en löv och en rot första gången man begär en licens för en viss dator. Om användaren redan har rotlicensen kan servern endast utfärda en löv (ring `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` för att avgöra om klienten redan har en 3.0 Förbättrad rot). För efterföljande licensbegäranden kommer klienten att ange att den redan har en löv och en rot, så servern bör utfärda en ny rotlicens. När den utökade licenskedjan används, `setRootKeyRetrievalInfo()` måste anropas för att ange de autentiseringsuppgifter som krävs för att dekryptera rotkrypteringsnyckeln i principen.

>[!NOTE]
>
>Om profilen har stöd för 3.0 Förbättrad licenskedning, men klienten är Adobe Access 2.0, kommer servern att utfärda en 2.0-original som kedjad licens. Använd LicenseRequestMessage.getClientVersion() för att fastställa klientversionen.
