---
seo-title: Domänregistrering för enhetsgrupp
title: Domänregistrering för enhetsgrupp
uuid: 221bf6c3-0568-443d-b761-64715a57ada6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Domänregistrering för enhetsgrupp{#device-group-domain-registration}

Som ett alternativ till att binda en licens till en viss enhet stöder Primetime DRM 3.0 eller senare bindning av licenser till en enhetsdomän.

Flera enheter kan ansluta till en domän och ta emot domäntoken. När en enhet i domänen har skaffat en licens kan licensen överföras till vilken annan enhet som helst i domänen, och dessa enheter kan spela upp innehållet utan att hämta en licens direkt från licensservern.

Om du vill ha stöd för domänbundna licenser måste DRM-principen för Primetime specificera den domänserver som klienten måste registrera med. DRM-principen Primetime måste också ange autentiseringskraven för domänservern om anonym åtkomst är aktiverat eller om servern kräver användarnamn/lösenord eller anpassad autentisering.

Domänregistrering och domänbundna licenser stöds av Primetime DRM-klienter version 3.0 eller senare. Om en äldre klient eller en Adobe Primetime 3.0-klient i Flash Player begär en licens för innehåll som stöder domänregistrering, kan licensservern utfärda en licens som använder en alternativ Primetime DRM-princip för att stödja bindning till en viss enhet.
