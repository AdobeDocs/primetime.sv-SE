---
seo-title: Använda en kodare från tredje part
title: Använda en kodare från tredje part
uuid: 8649303c-b8e6-4c02-a8ad-5734af850bfe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Använd en kodare från tredje part{#use-a-third-party-encoder}

Vissa kunder kanske redan har en pipeline för innehållsförberedelser på plats, som använder en maskinvaru- eller programvaruvideokodare (eller Adobe Media Server). Om så är fallet kan alla produkter som för närvarande kan skapa DRM-skyddat Primetime-innehåll paketera innehåll för Primetime Cloud DRM med samma konfigurationsinställningar som Primetime Cloud DRM Protection Kit. Nödvändig information kan hämtas från någon av de befintliga konfigurationsfilerna som ingår i paketet: [!DNL config_hls.xml] eller [!DNL config_hds.xml].

De relevanta konfigurationsobjekten är:

* Licensserverns URL
* URL för nyckelserver
* Licensservercertifikat
* Transportcertifikat

