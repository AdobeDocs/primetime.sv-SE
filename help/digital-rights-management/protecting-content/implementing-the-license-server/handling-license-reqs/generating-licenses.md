---
seo-title: Genererar licenser
title: Genererar licenser
uuid: f91b0cc8-e0ed-4722-947b-22eb2bfba916
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Genererar licenser{#generating-licenses}

Om du vill utfärda en lövlicens till en användare måste SDK dekryptera CEK-innehållet i innehållets metadata och kryptera om det för den dator som begär en licens. Om du vill dekryptera CEK:t måste servern ange den information som krävs för att dekryptera nyckeln. Anropa `ContentInfo.setKeyRetrievalInfo()` och ange ett `AsymmetricKeyRetrieval` objekt. Om metadata innehåller flera principer måste servern avgöra vilken princip som ska användas och anropas `LicenseRequestMessage.setSelectedPolicy()`. Ring sedan `LicenseRequestMessage.generateLicense()` för att generera licensen. Med det `License` objekt som returneras kan du ändra licensens förfallodatum eller rättigheter.

Om ett `ExternalKeyRetrieval` objekt anges i `ContentInfo` objektet förväntas licensservern använda det associerade CK-ID:t för att hämta rätt CK som infogas i licensen.

Mer information om hur du använder arbetsflödet Externt CEK finns i [Adobe Primetime DRM External CEK Overview](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) .
