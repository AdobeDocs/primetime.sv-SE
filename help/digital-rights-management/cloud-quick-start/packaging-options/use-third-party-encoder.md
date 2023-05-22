---
title: Använda en kodare från tredje part
description: Använda en kodare från tredje part
copied-description: true
exl-id: 565f69db-8595-4f78-b1e6-26f277a3784a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
