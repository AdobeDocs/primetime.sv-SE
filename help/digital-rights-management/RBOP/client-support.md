---
description: I det här avsnittet beskrivs de funktioner som finns i olika versioner av Flash Player och TVSDK.
seo-description: I det här avsnittet beskrivs de funktioner som finns i olika versioner av Flash Player och TVSDK.
seo-title: Stöd för RBOP-klient
title: Stöd för RBOP-klient
uuid: d1d0f788-7bc1-488c-807e-be47f83725e9
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---


# Stöd för RBOP-klient {#rbop-client-support}

I det här avsnittet beskrivs de funktioner som finns i olika versioner av Flash Player och TVSDK.

**Felutsändning** - TVSDK-plattformarna som anges nedan skickar ett DRM-körningsfel när upplösningen för det innehåll som spelas upp överskrider den tillåtna upplösningen för enhetskonfigurationen som definieras i DRM-principen:

* Flash Player version 18 till 20
* Android - versioner
* iOS - versioner

>[!NOTE]
>
>* Alla Flash- och mobilplattformar har stöd för Error Dispatch, men endast de TVSDK-klienter som anges ovan bearbetar RBOP-relaterade fel.
>* RBOP-relaterade [DRM-klientfel](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
   >    * **3371** - Felaktig upplösning baserad på begränsningar för utdataskydd i licensen.
   >    * **3372** - Innehållets upplösning är större än den maximala upplösning som anges i utdataskyddsbegränsningen. (Detta kan inträffa om någon försöker injicera innehåll som är avsett för en annan enhet.)
   >    * **3373** - Innehållets upplösning är större än den upplösning som anges av det aktiva utdataskyddsvillkoret. (Det innebär att vi måste nedgradera.)

>



**Automatisk nedskalning** - Tekniken som används för nedskalning varierar beroende på plattform och Flash Player-version:

* Flash Player version 21: Stöder RBOP med automatisk nedskalning (intelligent bitrate-växling)
* Firefox version 38 och senare på Windows (med Access CDM): Adobe nedgraderar automatiskt en högre bithastighetsström till en lägre (till skillnad från nedladdning av en låggradsström).

>[!NOTE]
>
>De här plattformarna gör automatiskt video nedskalat och visar innehållet med en upplösning som är lägre än eller lika med vad som anges i DRM-principen. Med den här funktionen spelas innehåll alltid upp till klienten, så länge det finns en tillgänglig ström som uppfyller DRM-principbegränsningarna.

**Äldre utdataskydd** - Klienter som använder Flash Player före version 18 kan bara hantera äldre OP-begränsningar. Klienter med Flash Player version 18 och senare kan hantera antingen äldre eller RBOP-begränsningar. Om du anger RBOP-begränsningar bör du även ange äldre OP-begränsningar för äldre klienter. För klienter som stöder RBOP överskrider RBOP-begränsningarna de gamla begränsningarna för OP.
