---
description: 'null'
seo-description: 'null'
seo-title: Enhetsfunktioner som krävs för att spela upp skyddat innehåll
title: Enhetsfunktioner som krävs för att spela upp skyddat innehåll
uuid: 1490711b-65d9-4716-8779-ae1da7d2c82c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# Enhetsfunktioner som krävs för att spela upp skyddat innehåll {#device-capabilities-required-to-play-protected-content}

Nödvändiga enhetsfunktioner anger vilka maskinvarufunktioner som krävs för att komma åt innehållet. Information om maskinvarufunktionerna finns tillgänglig för enheter som använder porteringsverktyget.

Följande attribut kan identifiera enhetsfunktionerna:

<table id="table_v3n_fks_n4"> 
 <tbody> 
  <tr> 
   <td><b>Attribut</b> </td> 
   <td><b>Värden som stöds</b> </td> 
   <td><b>Matcha villkor</b> </td> 
   <td><b>Beskrivning</b> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Buss som inte är tillgänglig för användare </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" eller "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Exakt matchning </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Om true får enheten inte ha en buss som är tillgänglig för användaren. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Maskinvarurot för förtroende </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">"true" eller "false" </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Exakt matchning </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Om true måste enheten ha en maskinvarurot som är betrodd. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Den här användningsregeln stöds av Adobe Primetime DRM-klienter version 2.0.2 och senare. Beteendet för äldre klienter beror på den lägsta klientversion som stöds av licensservern.
>
>Se [Minimal klientversion](../../../../protecting-content/setting-up-the-sdk/setup-dev-env.md).

