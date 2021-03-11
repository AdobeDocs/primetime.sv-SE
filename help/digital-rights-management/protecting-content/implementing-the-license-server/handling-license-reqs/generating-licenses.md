---
title: Genererar licenser
description: Genererar licenser
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Genererar licenser{#generating-licenses}

Om du vill utfärda en lövlicens till en användare måste SDK dekryptera CEK-innehållet i innehållets metadata och kryptera om det för den dator som begär en licens. Om du vill dekryptera CEK:t måste servern ange den information som krävs för att dekryptera nyckeln. Anropa `ContentInfo.setKeyRetrievalInfo()` och ange ett `AsymmetricKeyRetrieval`-objekt. Om metadata innehåller flera principer måste servern avgöra vilken princip som ska användas och anropa `LicenseRequestMessage.setSelectedPolicy()`. Ring sedan `LicenseRequestMessage.generateLicense()` för att generera licensen. Med `License`-objektet som returneras kan du ändra licensens förfallodatum eller rättigheter.

Om ett `ExternalKeyRetrieval`-objekt anges i `ContentInfo`-objektet förväntas licensservern använda det associerade CEK-ID:t för att hämta rätt CEK som infogas i licensen.

Mer information om hur du använder det externa CEK-arbetsflödet finns i [Adobe Primetime DRM External CEK Overview](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md).
