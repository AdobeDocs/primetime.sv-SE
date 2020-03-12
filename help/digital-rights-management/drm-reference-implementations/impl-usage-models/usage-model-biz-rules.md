---
description: 'null'
seo-description: 'null'
seo-title: Affärsregler för demonstration av användningsmodell
title: Affärsregler för demonstration av användningsmodell
uuid: c55f85be-5ecb-4a78-b47d-7001ec207d3a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Affärsregler för demonstration av användningsmodell{#usage-model-demo-business-rules}

När en användare begär en licens kontrollerar Reference Implementation-servern de metadata som klienten har skickat för att avgöra om innehållet paketerades med egenskapen `RI_UsageModelDemo` . I så fall tillämpar servern följande affärsregler.

* Om någon av DRM-profilerna kräver autentisering:

   * Om begäran innehåller en giltig autentiseringstoken söker du efter användarens namn i kunddatabastabellen.

      Om du inte hittar namnet på användaren utför du följande åtgärder:

      * Om `Customer.IsSubscriber` egenskapen är inställd på `true`måste du generera en licens för *`Subscription`* användningsmodellen och skicka den till användaren.

      * Sök efter en post i databastabellen efter användarens namn och innehålls-ID:t `CustomerAuthorization` .
      Om du kan hitta användarens post utför du följande åtgärder:

      * Om `CustomerAuthorization.UsageType` egenskapen är inställd på `DTO`skapar du en licens för DTO-användningsmodellen och skickar den till användaren.

      * Om `CustomerAuthorization.UsageType` egenskapen är inställd på `VOD`skapar du en licens för VOD-användningsmodellen och skickar den till användaren.
      Om ingen DRM-princip tillåter anonym åtkomst utför du följande åtgärder:

      * Om det inte finns någon giltig autentiseringstoken i begäran måste du returnera felet &quot;autentisering krävs&quot;.
      * Annars returneras ett &quot;ej auktoriserat&quot; fel.



* Om någon av DRM-profilerna tillåter anonym åtkomst skapar du en licens för den annonsfinansierade användningsmodellen och skickar den till användaren.

