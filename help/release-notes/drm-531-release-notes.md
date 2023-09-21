---
title: Versionsinformation om DRM 5.3.1
description: Versionsinformationen för DRM 5.3.1 beskriver de nya funktionerna och de kända problemen i DRM 5.3.1.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Versionsinformation om DRM 5.3.1 {#drm-release-notes}

Versionsinformationen för DRM 5.3.1 beskriver de nya funktionerna och de kända problemen i DRM 5.3.1.

## Nya funktioner i version 5.3 {#new-features}

* **Säkert stopp -** Du kan ange om uppspelningen ska stoppas eller fortsätta i slutet av uppspelningsfönstret.
* **RBOP (Resolution Based Output Protection) -** Du kan ange utdatabegränsningar baserat på pixelupplösningar.
* **CDM Gating -** För att stödja HTML5 har Adobe uppdaterat referensimplementeringslicensservern som ingår i Java SDK för Adobe Primetime DRM (tidigare Adobe Access DRM) så att alla DRM-protokollmeddelanden kan användas vid en enda URL-slutpunkt. Denna konsolidering av HTTP URL-metoder är nödvändig för att uppfylla specifikationen HTML5 EME (Encrypted Media Extension) som i sin tur måste implementeras av CDM-leverantörer (Content Decryption Module) för DRM. Tidigare var detta de enda URL-slutpunkterna som exponerades av licensservern för referensimplementering:

   * /flashaccess/i15n/v3 (Individualisering)
   * /flashaccess/license/v5 (licensbegäran)
   * /flashaccess/licenseRet/v5 (licensretur)
   * /flashaccess/getServerVersion/v5 (Hämta serverversion)

Nu kan alla begäranden (som kommer från en CDM i HTML5) dirigeras till en enda slutpunkt: /req

Den här ändringen är bakåtkompatibel med andra plattformar än CDM, till exempel Flash Player, Android och iOS.

* **RBOP-nedskalning -** RBOP är specifikt för HTML5-rymden och innehåller automatisk nedskalning. Om en bithastighet som överskrider den tillåtna bithastigheten som anges i DRM-principen kommer innehållet att nedskalas till den högsta tillåtna upplösningen. Om till exempel en 1080p-ström direktuppspelas till en klient som visar innehållet på en bildskärm som inte är HDCP-kompatibel, kan DRM-principen indikera att den maximala upplösningen ska vara 720p. Primetime DRM avkodar 1080p-strömmen och nedskalar den sedan till 720p innan den återges på skärmen. Om webbläsaren som spelar upp videon sedan dras över till en bildskärm som har stöd för HDCP, kommer Primetime DRM att avbryta nedskalningen av innehållet och tillåta uppspelning vid 1080.

## Kända fel i version 5.3 {#known-issues}

* `Hasher.bat (flashaccess-hasher.jar)` skickar loggmeddelanden till `flashaccess-global.log.`Du måste se till att `flashaccess-global.log` filen finns i samma katalog som Hasher.bat.

* Utdata från vissa av `toJSON()`anrop returnerar `Strings` som inte är helt JSON-kompatibla eller helt kompatibla på ett fristående sätt (dvs. utan sammansättning av JSON-strukturer).

* Xbox-nyckelservern accepterar nyckelbegäranden som har ett versionsvärde som inte är lika med 1.

Xbox-nyckelservern bör bara ha stöd för nyckelförfrågningar som har versionen 1, men för närvarande accepterar servern nyckelförfrågningar där versionen inte är 1.

* Xbox-nyckelservern validerar inte en princip korrekt.

Xbox-nyckelservern bör inte acceptera principer som ligger utanför giltighetsdatumet, men för närvarande accepterar servern dem oavsett.

* Xbox-nyckelservern bör avvisa en nyckelbegäran som innehåller metadata som har skapats med fel paketerarcertifikat.
* Returnerat värde för vissa JSON-strukturer är inte korrekt formaterade för upplösningsbaserade Output Protection-relaterade klasser.

Flera klasser implementerar en toJSON()-metod som ska returnera en JSON-kompatibel representation av det objektet som en sträng, men det returnerade värdet är för närvarande inte helt JSON-kompatibelt.

## Användbara resurser {#helpful-resources}

* Se den fullständiga hjälpdokumentationen på [Adobe Primetime Läs mer &amp; Support](https://helpx.adobe.com/support/primetime.html) sida.
