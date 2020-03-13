---
description: Vanligtvis är alla Primetime DRM-licenser bundna till en unik enhet när de skapas. Denna bindning förhindrar att användare delar licenser mellan olika enheter utan behörighet. Förutom bindning per enhet ger Primetime DRM möjlighet att binda licenser till en enhetsdomän eller grupp av enheter.
seo-description: Vanligtvis är alla Primetime DRM-licenser bundna till en unik enhet när de skapas. Denna bindning förhindrar att användare delar licenser mellan olika enheter utan behörighet. Förutom bindning per enhet ger Primetime DRM möjlighet att binda licenser till en enhetsdomän eller grupp av enheter.
seo-title: Spela upp krypterat innehåll med domänstöd
title: Spela upp krypterat innehåll med domänstöd
uuid: 8854cc0f-9bfc-4833-82d7-a3f46ac88e06
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Stöd för enhetsdomän {#device-domain-support}

Vanligtvis är alla Primetime DRM-licenser bundna till en unik enhet när de skapas. Denna bindning förhindrar att användare delar licenser mellan olika enheter utan behörighet. Förutom bindning per enhet ger Primetime DRM möjlighet att binda licenser till en enhetsdomän eller grupp av enheter.

Om innehållets metadata anger att enhetsdomänregistrering krävs, kan programmet anropa ett API för att ansluta till en enhetsgrupp. Den här åtgärden utlöser en begäran om domänregistrering som ska skickas till domänservern. När en licens har utfärdats till en enhetsgrupp kan licensen exporteras och delas med andra enheter som har anslutit till enhetsgruppen.

Informationen om enhetsgruppen används sedan i `DRMContentData` `VoucherAccessInfo` objektet, som sedan används för att presentera den information som krävs för att hämta och använda en licens.

## Spela upp krypterat innehåll med domänstöd {#play-encrypted-content-using-domain-support}

Så här spelar du upp krypterat innehåll med Primetime DRM:

1. Använd `VoucherAccessInfo.deviceGroup`och kontrollera om enhetsgruppsregistrering krävs.
1. Om autentisering krävs:
   1. Använd egenskapen för att ta reda på `DeviceGroupInfo.authenticationMethod` om autentisering krävs.
   1. Om autentisering krävs autentiserar du användaren genom att utföra NÅGOT av följande steg:

      * Hämta användarens användarnamn och lösenord och anropa `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Hämta en cachelagrad/förgenererad autentiseringstoken och anropa `DRMManager.setAuthenticationToken()`.
   1. Anropa `DRMManager.addToDeviceGroup()`
1. Hämta licensen för innehållet genom att utföra någon av följande åtgärder:
   1. Använd `DRMManager.loadVoucher()` metoden.
   1. Skaffa licensen från en annan enhet som är registrerad i samma enhetsgrupp och leverera licensen till ` DRMManager` via `DRMManager.storeVoucher()` metoden.
1. Spela upp det krypterade innehållet med `Primetime.play()` metoden .
Om du vill exportera licensen för innehållet kan alla enheter tillhandahålla licensens råa-byte med hjälp av `DRMVoucher.toByteArray()` metoden efter att licensen har hämtats från Primetimes DRM-licensserver. Innehållsleverantörer begränsar vanligtvis antalet enheter i en enhetsgrupp. Om gränsen nås kan du behöva anropa metoden på en enhet som inte används innan du registrerar den aktuella enheten. `DRMManager.removeFromDeviceGroup()`