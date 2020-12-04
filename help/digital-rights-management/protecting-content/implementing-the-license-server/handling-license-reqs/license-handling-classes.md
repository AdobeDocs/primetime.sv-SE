---
seo-title: Översikt
title: Översikt
uuid: 2bbf0aa1-df35-429d-84df-db357fa53e47
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Översikt {#overview}

För att erhålla en licens skickar klienterna en begäran från de metadata som är inbäddade i det paketerade innehållet och skickar sedan begäran till licensservern. Licensservern använder information som hämtats från innehållets metadata för att generera en licens.

Om både klienten och servern stöder protokollversion 5 är URL:en för begäran &quot;License Server i metadata&quot; + &quot; [!DNL /flashaccess/license/v4]&quot;. Om protokollversion 3 är den maximala som stöds av antingen klienten eller servern skickar Primetime DRM-klienter sedan autentiseringsbegäranden till &quot;License Server URL in metadata&quot; + &quot; [!DNL /flashaccess/license/v3]&quot;. Annars skickas autentiseringsbegäranden till licensserverns URL i metadata + [!DNL /flashaccess/license/v1]

En enhet kan ha flera licenser för samma innehåll (samma licens-ID), men kan bara ha en licens för ett visst licens-ID och DRM-princip-ID. Om den får en licens med ett duplicerat LicenseID/PolicyID ersätter den nya licensen bara den gamla om den nya licensens utfärdandedatum infaller senare än den befintliga licensens utfärdandedatum. Den här logiken används för att bearbeta licenser som är inbäddade i innehållet. Därför bör du inte bädda in mer än en licens med samma DRM-princip-ID i ett innehållssegment. Samma logik gäller för licenser som skickas till klienten via ActionScript3-API:t `DRMManager.storeVoucher()`. Om klienten redan har en licens med ett senare utfärdandedatum kan den angivna licensen ignoreras.

## Hanteringsklasser för licensbegäran {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler` - Det här är hanterarklassen för licensbegäran. Det läser och tolkar licensförfrågningar. Dess `getRequests()`-metod returnerar en lista med `LicenseRequestMessage`-objekt.
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage` - Det här är meddelandeklassen för begäran. Anroparen bör iterera genom `LicenseRequestMessage`-listan som returneras av `getRequests()`, och för varje begäran ska antingen en licens genereras eller en felkod anges. Ring `LicenseRequestMessage.getContentInfo()` för att få information som extraherats från innehållets metadata, inklusive profil för innehålls-ID, licens-ID och DRM.

Licenser och fel skickas samtidigt när metoden `LicenseHandler.close()` anropas.

Mer information finns i [API-referensdokumentationen för DRM-servern](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html).
