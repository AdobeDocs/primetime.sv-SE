---
title: Affärsregler för demonstration av användningsmodell
description: Affärsregler för demonstration av användningsmodell
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Affärsregler för demonstration av användningsmodell{#usage-model-demo-business-rules}

När en användare begär en licens kontrollerar Reference Implementation-servern de metadata som klienten har skickat för att avgöra om innehållet paketerades med `RI_UsageModelDemo` -egenskap. I så fall tillämpar servern följande affärsregler.

* Om någon av DRM-profilerna kräver autentisering:

   * Om begäran innehåller en giltig autentiseringstoken söker du efter användarens namn i kunddatabastabellen.

     Om du inte hittar namnet på användaren utför du följande åtgärder:

      * Om `Customer.IsSubscriber` egenskapen är inställd på `true`måste du generera en licens för *`Subscription`* användningsmodell och skicka den till användaren.

      * Sök efter en post i `CustomerAuthorization` databastabell för användarens namn och innehålls-ID.

     Om du kan hitta användarens post utför du följande åtgärder:

      * Om `CustomerAuthorization.UsageType` egenskapen är inställd på `DTO`, generera en licens för DTO-användningsmodellen och skicka den till användaren.

      * Om `CustomerAuthorization.UsageType` egenskapen är inställd på `VOD`, generera en licens för VOD-användningsmodellen och skicka den till användaren.

     Om ingen DRM-princip tillåter anonym åtkomst utför du följande åtgärder:

      * Om det inte finns någon giltig autentiseringstoken i begäran måste du returnera felet &quot;autentisering krävs&quot;.
      * Annars returneras ett &quot;ej auktoriserat&quot; fel.

* Om någon av DRM-profilerna tillåter anonym åtkomst skapar du en licens för den annonsfinansierade användningsmodellen och skickar den till användaren.
