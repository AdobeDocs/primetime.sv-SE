---
title: Översikt över out-of-band-licenser
description: Översikt över out-of-band-licenser
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Out-of-band-licenser {#out-of-band-licenses}

Licenser kan också erhållas utan att man behöver kontakta en Primetime DRM-licensserver genom att lagra licensen på disken och i minnet med `storeVoucher()` -metod.

Om du vill spela upp krypterade videor i Primetime måste respektive körningsmiljö erhålla licensen för videon. Licensen innehåller videons dekrypteringsnyckel och genereras av den DRM-licensserver för Primetime som kunden har distribuerat.

Körningsmiljön erhåller vanligtvis den här licensen genom att skicka en licensbegäran till DRM-licensservern för Primetime som anges i videons DRM-metadata ( `DRMContentData` klass). Programmet kan utlösa denna licensbegäran genom att anropa `DRMManager.loadVoucher()` -metod.

`DRMManager.storeVoucher()` gör att programmet kan skicka licenser som det har fått utan band. Körningsmiljön kan sedan hoppa över licensförfrågningsprocessen och använda de vidarebefordrade licenserna för att spela upp krypterade videofilmer. Licensen måste fortfarande genereras av Primetimes DRM-licensserver innan den kan hämtas utan band. Du kan dock välja att lagra licenserna på valfri HTTP-server i stället för på en Primetime DRM-licensserver.

`DRMManager.storeVoucher()` används också för att stödja licensdelning mellan olika enheter. Efter Primetime DRM 3.0 kallas den här funktionen för stöd för enhetsdomäner. Om din distribution har stöd för det här användningsfallet kan du registrera flera datorer till en enhetsgrupp med `DRMManager.addToDeviceGroup()` -metod. Om det finns en dator med en giltig domänbunden licens för ett visst innehåll, kan programmet extrahera den serialiserade licensen med `DRMVoucher.toByteArray()` och på dina andra datorer kan du importera licenserna med `DRMManager.storeVoucher()` -metod.

## Om enhetsregistrering {#about-device-registration}

Alla Primetime DRM-licenser måste vara bundna till en slutenhet när de skapas. Bindning är den kryptografiska processen som innebär att endast en viss enhet kan använda licensen. Detta är nödvändigt för att förhindra&quot;svävande licenser&quot; som kan användas av valfri enhet. För Primetime DRM att&quot;förgenerera&quot; licenser innebär detta att&quot;målet&quot; för dessa förgenererade licenser måste vara känt i förväg. Primetime DRM refererar till detta som&quot;Device Registration&quot;.

## Registrera en enhet {#register-a-device}

Låt oss anta att du har utfört följande uppgifter:

* Du har konfigurerat Primetime DRM Server SDK.
* Du har konfigurerat en HTTP-server för att utfärda förgenererade licenser.
* Du har skapat ett Primetime-program för att visa det skyddade innehållet.

 Enhetsregistreringsfasen omfattar följande åtgärder:

1. Programmet skapar ett slumpmässigt genererat ID.
1. Programmet anropar `DRMManager.authenticate()` -metod. Programmet måste inkludera det slumpmässigt genererade ID:t i autentiseringsbegäran. Ta till exempel med ID:t i fältet för användarnamn.
1. Åtgärden som nämns i steg 2 resulterar i att Primetime DRM skickar en autentiseringsbegäran till kundens server. Denna begäran innehåller enhetscertifikatet:
   1. Servern extraherar enhetscertifikatet och det genererade ID:t från begäran och lagrar.
   1. Kundens undersystem genererar i förväg licenser för det här enhetscertifikatet, lagrar dem och beviljar åtkomst till dem på ett sätt som associerar dem med det genererade ID:t. .
1. Servern svarar på begäran med meddelandet&quot;success&quot;.
1. Programmet lagrar det genererade ID:t.

Efter enhetsregistreringen använder programmet det genererade ID:t på samma sätt som det skulle ha använt enhets-ID:t i det tidigare schemat:
1. Programmet försöker hitta det genererade ID:t.
1. Om det genererade ID:t hittas kommer programmet att använda det genererade ID:t när de förgenererade licenserna hämtas. Programmet skickar licenserna till Primetime DRM-klienten för konsumtion med `DRMManager.storeVoucher()` -metod. .
1. Om det genererade ID:t inte hittas går programmet igenom enhetsregistreringsproceduren.

## DRM-fabriksåterställning {#drm-factory-reset}

När användaren av enheten anropar alternativet DRM-fabriksåterställning rensas enhetscertifikatet. Om du vill fortsätta spela upp det skyddade innehållet måste programmet gå igenom enhetsregistreringsproceduren igen. Om programmet skickar en inaktuell förgenererad licens, kommer Primetime DRM-klienten att avvisa den eftersom licensen krypterades för ett äldre enhets-ID.

* Flash-API: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers()) - (Kan endast anropas som svar på vissa DRM-felkoder som inte kan återställas.)
* iOS API: [DRMManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* Android API: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))
