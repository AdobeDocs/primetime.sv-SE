---
seo-title: Genererar licenser
title: Genererar licenser
uuid: 242d5567-f609-4781-a8a6-2f3d78471344
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Genererar licenser {#generating-licenses}

Om du vill utfärda en lövlicens till användaren måste SDK dekryptera CEK:n som finns i innehållets metadata och kryptera om den för datorn som begär en licens. Om du vill dekryptera CEK:t måste servern ange den information som krävs för att dekryptera nyckeln. Anropa `ContentInfo.setKeyRetrievalInfo()` och ange ett `AsymmetricKeyRetrieval` objekt. Om metadata innehåller flera principer måste servern avgöra vilken princip som ska användas och anropas `LicenseRequestMessage.setSelectedPolicy()`. Ring sedan `LicenseRequestMessage.generateLicense()` för att generera licensen. Med det `License` objekt som returneras kan du ändra licensens förfallodatum eller rättigheter.

Om ett ExternalKeyRetrieval-objekt anges i `ContentInfo` objektet, förväntas licensservern använda det associerade CEK-ID:t för att hämta rätt CEK som ska infogas i licensen. Mer information om hur du använder det externa CEK-arbetsflödet finns i Översikt över [Adobe Access DRM External CEK](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md)
