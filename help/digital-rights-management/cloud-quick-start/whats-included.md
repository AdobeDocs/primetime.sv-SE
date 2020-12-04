---
description: Adobe tillhandahåller en molntjänst för DRM till Adobe Primetime DRM-kunder som inte vill utveckla och underhålla sin egen Primetime DRM-licensserver. Genom att använda den här tjänsten kan kunderna minska komplexiteten vad gäller drift och utveckling i samband med utfärdandet av DRM-licenser. Primetime Cloud DRM kan utfärda DRM-licenser till alla enheter som kan köra en Primetime Browser TVSDK-aktiverad videoapplikation, som iOS, Android, stationära datorer och Xbox360. Den här DRM-tjänsten hanteras av Adobe, med drifttid dygnet runt.
seo-description: Adobe tillhandahåller en molntjänst för DRM till Adobe Primetime DRM-kunder som inte vill utveckla och underhålla sin egen Primetime DRM-licensserver. Genom att använda den här tjänsten kan kunderna minska komplexiteten vad gäller drift och utveckling i samband med utfärdandet av DRM-licenser. Primetime Cloud DRM kan utfärda DRM-licenser till alla enheter som kan köra en Primetime Browser TVSDK-aktiverad videoapplikation, som iOS, Android, stationära datorer och Xbox360. Den här DRM-tjänsten hanteras av Adobe, med drifttid dygnet runt.
seo-title: Bakgrund
title: Bakgrund
uuid: 11a5b9ea-ebd2-47e0-b078-af2a3e1f7bf6
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# Bakgrund {#background}

Adobe tillhandahåller en molntjänst för DRM till Adobe Primetime DRM-kunder som inte vill utveckla och underhålla sin egen Primetime DRM-licensserver. Genom att använda den här tjänsten kan kunderna minska komplexiteten vad gäller drift och utveckling i samband med utfärdandet av DRM-licenser. Primetime Cloud DRM kan utfärda DRM-licenser till alla enheter som kan köra en Primetime Browser TVSDK-aktiverad videoapplikation, som iOS, Android, stationära datorer och Xbox360. Den här DRM-tjänsten hanteras av Adobe, med drifttid dygnet runt.

>[!NOTE]
>
>Adobe Primetime DRM kallades tidigare Adobe Access och tidigare Flash Access.

## Vad ingår i Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}?

* Anpassad autentiserings-/berättigandemodul och instruktioner för hur du kan aktivera anpassad autentisering för ditt innehåll. Mer information finns i katalogen [!DNL Custom Authentication Entitlement].
* DRM-specifikt molnlicensservercertifikat ( [!DNL .pem/.cer/.der])

* Transportcertifikat för molnspecifik DRM-specifik licensserver ( [!DNL .pem/.cer/.der])

* Primetime Java Offline Packager
* Exempel på DRM-principer för paketering

   * **policy_24hr**  - Licenser finns på disken i 24 timmar. Efter 24 timmar måste man skaffa en ny licens för att kunna se innehållet. Alla andra policyer i det här paketet har även 24 timmars cache-lagring av licenser.
   * **policy_ios_remotekeyserver** - På iOS-enheter hämtas DRM-licensen från molnet-DRM. Dessutom kommer klienten att hämta alla AES-dekrypteringsnycklar från molnet-DRM. Uppspelning tillåts inte på jailbroken iOS-enheter.

   * **policy_ios_localkeyserver** - På iOS-enheter hämtas DRM-licensen från molnet-DRM. Dessutom kommer klienten att hämta alla HLS AES-dekrypteringsnycklar från en lokal HTTP-server i stället för molnbaserad DRM. Uppspelning tillåts inte på jailbroken iOS-enheter.

   * **policy_adobePass** - Klienten måste först autentisera med (tidigare kallat Adobe Pass), annars nekas en licens.

* Adobe Policy Manager-verktyg för att skapa ytterligare DRM-principer
* Exempelvideoinnehåll som ska användas för paketering

