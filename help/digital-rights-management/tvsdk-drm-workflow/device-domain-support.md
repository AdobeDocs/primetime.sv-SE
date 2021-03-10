---
description: Vanligtvis är alla Primetime DRM-licenser bundna till en unik enhet när de skapas. Denna bindning förhindrar att användare delar licenser mellan olika enheter utan behörighet. Förutom bindning per enhet ger Primetime DRM möjlighet att binda licenser till en enhetsdomän eller grupp av enheter.
title: Spela upp krypterat innehåll med domänstöd
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Stöd för enhetsdomän {#device-domain-support}

Vanligtvis är alla Primetime DRM-licenser bundna till en unik enhet när de skapas. Denna bindning förhindrar att användare delar licenser mellan olika enheter utan behörighet. Förutom bindning per enhet ger Primetime DRM möjlighet att binda licenser till en enhetsdomän eller grupp av enheter.

Om innehållets metadata anger att enhetsdomänregistrering krävs, kan programmet anropa ett API för att ansluta till en enhetsgrupp. Den här åtgärden utlöser en begäran om domänregistrering som ska skickas till domänservern. När en licens har utfärdats till en enhetsgrupp kan licensen exporteras och delas med andra enheter som har anslutit till enhetsgruppen.

Informationen om enhetsgruppen används sedan i `DRMContentData` `VoucherAccessInfo`-objektet, som sedan används för att presentera den information som krävs för att hämta och använda en licens.

## Spela upp krypterat innehåll med domänstöd {#play-encrypted-content-using-domain-support}

Så här spelar du upp krypterat innehåll med Primetime DRM:

1. Använd `VoucherAccessInfo.deviceGroup` och kontrollera om enhetsgruppsregistrering krävs.
1. Om autentisering krävs:
   1. Använd egenskapen `DeviceGroupInfo.authenticationMethod` för att ta reda på om autentisering krävs.
   1. Om autentisering krävs autentiserar du användaren genom att utföra NÅGOT av följande steg:

      * Hämta användarens användarnamn och lösenord och anropa `DRMManager.authenticate(deviceGroup.serverURL, deviceGroup.domain, username, password)`.
      * Hämta en cachelagrad/förgenererad autentiseringstoken och anropa `DRMManager.setAuthenticationToken()`.
   1. Anropa `DRMManager.addToDeviceGroup()`
1. Hämta licensen för innehållet genom att utföra någon av följande åtgärder:
   1. Använd metoden `DRMManager.loadVoucher()`.
   1. Hämta licensen från en annan enhet som är registrerad i samma enhetsgrupp och ge licensen till ` DRMManager` genom metoden `DRMManager.storeVoucher()`.
1. Spela upp det krypterade innehållet med metoden `Primetime.play()`.
Om du vill exportera licensen för innehållet, kan alla enheter tillhandahålla licensens rå-byte med metoden `DRMVoucher.toByteArray()` efter att licensen har hämtats från Primetimes DRM-licensserver. Innehållsleverantörer begränsar vanligtvis antalet enheter i en enhetsgrupp. Om gränsen nås kan du behöva anropa metoden `DRMManager.removeFromDeviceGroup()` på en oanvänd enhet innan du registrerar den aktuella enheten.