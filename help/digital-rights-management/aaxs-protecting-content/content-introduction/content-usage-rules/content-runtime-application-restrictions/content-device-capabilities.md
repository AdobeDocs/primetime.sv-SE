---
seo-title: Enhetsfunktioner som krävs för att spela upp skyddat innehåll
title: Enhetsfunktioner som krävs för att spela upp skyddat innehåll
uuid: 16ed73d9-e02f-4c86-bf15-2d3e7122bf5a
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Enhetsfunktioner som krävs för att spela upp skyddat innehåll {#device-capabilities-required-to-play-protected-content}

Anger vilka maskinvarufunktioner som krävs för att komma åt innehåll. Information om maskinvarufunktionerna finns tillgänglig för enheter som använder porteringsverktyget.

Enhetens funktioner kan identifieras med de attribut som anges i följande tabell:

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
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">Exakt Macth </p> </td> 
   <td colname="4" class="- topic/entry "> <p class="- topic/p ">Om true måste enheten ha en maskinvarurot som är betrodd. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE] {class=&quot;- topic/note &quot;
>
>Den här användningsregeln stöds av Adobe Access-klienter version 2.0.2 och senare. Beteendet för äldre klienter beror på den lägsta klientversion som stöds av licensservern. Se [Minimal klientversion](../../../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md).

