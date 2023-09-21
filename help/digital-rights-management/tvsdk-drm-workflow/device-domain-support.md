---
description: Vanligtvis är alla Primetime DRM-licenser bundna till en unik enhet när de skapas. Denna bindning förhindrar att användare delar licenser mellan olika enheter utan behörighet. Förutom bindning per enhet ger Primetime DRM möjlighet att binda licenser till en enhetsdomän eller grupp av enheter.
title: Spela upp krypterat innehåll med domänstöd
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Stöd för enhetsdomän {#device-domain-support}

Vanligtvis är alla Primetime DRM-licenser bundna till en unik enhet när de skapas. Denna bindning förhindrar att användare delar licenser mellan olika enheter utan behörighet. Förutom bindning per enhet ger Primetime DRM möjlighet att binda licenser till en enhetsdomän eller grupp av enheter.

Om innehållets metadata anger att enhetsdomänregistrering krävs, kan programmet anropa ett API för att ansluta till en enhetsgrupp. Den här åtgärden utlöser en begäran om domänregistrering som ska skickas till domänservern. När en licens har utfärdats till en enhetsgrupp kan licensen exporteras och delas med andra enheter som har anslutit till enhetsgruppen.

Informationen om enhetsgruppen används sedan i `DRMContentData` `VoucherAccessInfo` -objekt, som sedan används för att presentera den information som krävs för att hämta och använda en licens.

## Spela upp krypterat innehåll med domänstöd {#play-encrypted-content-using-domain-support}

Så här spelar du upp krypterat innehåll med Primetime DRM:

1. Använda `VoucherAccessInfo.deviceGroup`kontrollerar du om enhetsgruppsregistrering krävs.
1. Om autentisering krävs:
   1. Använd `DeviceGroupInfo.authenticationMethod` egenskapen tar reda på om autentisering krävs.
   1. Om autentisering krävs autentiserar du användaren genom att utföra ETT av följande steg:

      * Hämta användarens användarnamn och lösenord och anropa `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Hämta en cachelagrad/förgenererad autentiseringstoken och anropa `DRMManager.setAuthenticationToken()`.

   1. Anropa `DRMManager.addToDeviceGroup()`
1. Hämta licensen för innehållet genom att utföra någon av följande åtgärder:
   1. Använd `DRMManager.loadVoucher()` -metod.
   1. Skaffa licensen från en annan enhet som är registrerad i samma enhetsgrupp och leverera licensen till `DRMManager` via `DRMManager.storeVoucher()` -metod.
1. Spela upp det krypterade innehållet med `Primetime.play()` -metod.
Om du vill exportera licensen för innehållet, kan alla enheter tillhandahålla licensens råa byte med `DRMVoucher.toByteArray()` efter att licensen erhållits från Primetimes DRM-licensserver. Innehållsleverantörer begränsar vanligtvis antalet enheter i en enhetsgrupp. Om gränsen nås kan du behöva ringa `DRMManager.removeFromDeviceGroup()` på en oanvänd enhet innan den aktuella enheten registreras.
