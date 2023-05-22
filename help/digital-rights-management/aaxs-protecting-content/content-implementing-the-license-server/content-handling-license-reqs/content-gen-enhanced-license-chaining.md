---
title: Förbättrad licenskedja
description: Förbättrad licenskedja
copied-description: true
exl-id: 4548cdc4-4a55-411b-ad22-8c77927f4564
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Förbättrad licenskedja {#enhanced-license-chaining}

Med förbättrad kedja av licenser i Adobe Access 3.0 rekommenderar vi att man utfärdar både en löv och en rot första gången man begär en licens för en viss dator. Om användaren redan har rotlicensen kan servern endast utfärda en löv (ring `LicenseRequestMessage.clientHasEnhancedRootForPolicy()` för att avgöra om klienten redan har en 3.0 Förbättrad rot). För efterföljande licensbegäranden anger klienten att den redan har en löv och en rot, så servern bör utfärda en ny rotlicens. När den utökade licenskedjan används, `setRootKeyRetrievalInfo()` måste anropas för att ange de autentiseringsuppgifter som krävs för att dekryptera rotkrypteringsnyckeln i principen.

>[!NOTE]
>
>Om profilen har stöd för 3.0 Förbättrad licenskedning, men klienten är Adobe Access 2.0, kommer servern att utfärda en 2.0-original som kedjad licens. Använd LicenseRequestMessage.getClientVersion() för att fastställa klientversionen.
