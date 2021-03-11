---
title: Om certifikat
description: Om certifikat
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Om certifikat {#about-certificates}

Adobe Primetime DRM SDK finns i följande konfigurationer:

* Primetime DRM Production SDK
* Primetime DRM Evaluation SDK
* Primetime DRM Trial SDK

Om du vill använda Primetime DRM SDK för att skapa en licensserver måste du skaffa digitala certifikat från Adobe. Digitala certifikat (kallas även certifikat) binder en enhet, till exempel en individ, organisation eller system, till ett specifikt nyckelpar för offentlig och privat nyckel. Digitala certifikat kan ses som elektroniska referenser som verifierar identiteten hos en individ, ett system eller en organisation.

För att ge maximal flexibilitet och utökad säkerhet i dina distributionsalternativ krävs fyra certifikat för Primetimes DRM SDK:

* Certifikat för licensserver

   SDK använder det här certifikatet för att signera innehållslicenser som utfärdas till klienter.
* Packager-certifikat

   SDK använder det här certifikatet för att generera DRM-metadata när innehåll paketeras (krypteras).
* Transportintyg

   SDK använder det här certifikatet för att säkra kommunikationen mellan klienterna och licensservern.
* Certifikat för domäncertifikatutfärdare

   Kunder som vill implementera en domänserver måste ha ett certifikatutfärdarcertifikat för domän. Till skillnad från andra certifikat utfärdas inte domänkontrollantcertifikatet av Adobe.

>[!NOTE]
>
>För SDK för utvärdering och SDK för testversion kombineras licensservern, Packager och transportcertifikaten till ett enda certifikat.

