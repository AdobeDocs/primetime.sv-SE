---
title: Använda en kodare från tredje part
description: Använda en kodare från tredje part
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Använda en kodare från tredje part{#use-a-third-party-encoder}

Vissa kunder kanske redan har en pipeline för innehållsförberedelser på plats, som använder en maskinvaru- eller programvaruvideokodare (eller Adobe Media Server). Om så är fallet kan alla produkter som för närvarande kan skapa DRM-skyddat Primetime-innehåll paketera innehåll för Primetime Cloud DRM med samma konfigurationsinställningar som Primetime Cloud DRM Protection Kit. Nödvändig information kan hämtas från någon av de befintliga konfigurationsfilerna som ingår i paketet: [!DNL config_hls.xml] eller [!DNL config_hds.xml].

De relevanta konfigurationsobjekten är:

* Licensserverns URL
* URL för nyckelserver
* Licensservercertifikat
* Transportcertifikat
