---
description: I det här avsnittet beskrivs de funktioner som finns i olika versioner av Flash Player och TVSDK.
title: Stöd för RBOP-klient
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Stöd för RBOP-klient {#rbop-client-support}

I det här avsnittet beskrivs de funktioner som finns i olika versioner av Flash Player och TVSDK.

**Felutsändning** - De TVSDK-plattformar som anges nedan skickar ett DRM-körningsfel när upplösningen för det innehåll som spelas upp överskrider den tillåtna upplösningen för enhetskonfigurationen som definieras i DRM-principen:

* Flash Player 18 till 20
* Android - versioner
* iOS - versioner

>[!NOTE]
>
>* Alla Flashs- och mobilplattformar har stöd för Error Dispatch, men endast de TVSDK-klienter som anges ovan bearbetar RBOP-relaterade fel.
>* RBOP-relaterade [DRM-klientfel](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
>    * **3371** - Felaktig upplösning baserad på begränsningar för utdataskydd i licensen.
>    * **3372** - Innehållets upplösning är större än den maximala upplösning som anges i utdataskyddsbegränsningen. (Detta kan inträffa om någon försöker injicera innehåll som är avsett för en annan enhet.)
>    * **3373** - Innehållets upplösning är större än den upplösning som anges av den aktuella utdataskyddsbegränsningen. (Det innebär att vi måste nedgradera.)
>

**Automatisk hämtning** - Tekniken som används vid nedskalning varierar beroende på plattform och Flash Player:

* Flash Player version 21: Stöder RBOP med automatisk nedskalning (intelligent bitrate-växling)
* Firefox version 38 och senare för Windows (med Access CDM): Adobe nedgraderar automatiskt en högre bithastighet till en lägre (till skillnad från nedladdning av en låggradig ström).

>[!NOTE]
>
>De här plattformarna gör automatiskt video nedskalat och visar innehållet med en upplösning som är lägre än eller lika med vad som anges i DRM-principen. Med den här funktionen spelas innehåll alltid upp till klienten, så länge det finns en tillgänglig ström som uppfyller DRM-principbegränsningarna.

**Äldre utdataskydd** - Klienter som använder Flashar Player som är äldre än version 18 kan bara hantera äldre OP-begränsningar. Klienter med Flash Player version 18 och senare kan hantera antingen äldre eller RBOP-begränsningar. Om du anger RBOP-begränsningar bör du även ange äldre OP-begränsningar för äldre klienter. För klienter som stöder RBOP överskrider RBOP-begränsningarna de gamla begränsningarna för OP.
