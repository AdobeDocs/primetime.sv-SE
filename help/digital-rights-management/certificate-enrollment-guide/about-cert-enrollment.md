---
title: Om certifikatregistreringsroller
description: Om certifikatregistreringsroller
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
