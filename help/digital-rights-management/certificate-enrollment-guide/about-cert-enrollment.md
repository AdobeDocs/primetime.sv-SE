---
title: Om certifikatregistreringsroller
description: Om certifikatregistreringsroller
copied-description: true
exl-id: fe3eb499-8636-46d0-8e5b-7baca08813bb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# Om certifikatregistreringsroller {#about-certificate-enrollment-roles}

Certifikatregistreringen kräver minst två anställda: en administratör och en beställare. Primetime DRM SDK-licenstagaren utser en kontoadministratör. Det får bara finnas en kontoadministratör. Kontoadministratören kan utse en sekundär administratör.

Administratörer kan utse upp till fem beställare. Beställare är anställda på företaget som begär och distribuerar certifikat. Administratörer godkänner certifikatbegäranden. Varje Adobe ID-konto kan bara ha en roll.

Följande är funktionerna för varje roll:

* Kontoadministratör

   * En kontoadministratör per licens
   * Lägg till beställare
   * Lägg till en sekundär administratör
   * Redigera telefoninformationen och svarsfrasen för det begärande företaget
   * Ta bort beställare och sekundära administratörer
   * Godkänn eller avvisa certifikatbegäranden
   * Återkalla utfärdade certifikat

* Sekundär administratör

   * En sekundär administratör per licens
   * Lägg till beställare
   * Redigera telefoninformationen och svarsfrasen för det begärande företaget
   * Ta bort beställare
   * Godkänn eller avvisa certifikatbegäranden
   * Återkalla utfärdade certifikat

* Beställare

   * Upp till fem beställare per licens
   * Begär certifikat
