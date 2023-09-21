---
title: Genererar licenser
description: Genererar licenser
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# Genererar licenser{#generating-licenses}

Om du vill utfärda en lövlicens till en användare måste SDK dekryptera CEK-innehållet i innehållets metadata och kryptera om det för den dator som begär en licens. Om du vill dekryptera CEK:t måste servern ange den information som krävs för att dekryptera nyckeln. Utlysning `ContentInfo.setKeyRetrievalInfo()` och tillhandahåller `AsymmetricKeyRetrieval` -objekt. Om metadata innehåller flera principer måste servern avgöra vilken princip som ska användas och anropa `LicenseRequestMessage.setSelectedPolicy()`. Ring sedan `LicenseRequestMessage.generateLicense()` för att generera licensen. Använda `License` som returneras kan du ändra licensens förfallodatum eller rättigheter.

Om en `ExternalKeyRetrieval` -objektet anges i `ContentInfo` -objektet, förväntas licensservern använda det associerade CK-ID:t för att hämta rätt CK som infogas i licensen.

Se [Adobe Primetime DRM External CEK Overview](../../../aaxs-drm-xkey-mgmt/aaxs-drm-using-external-cek-overview.md) om du vill ha mer information om hur du använder arbetsflödet för externt CEK.
