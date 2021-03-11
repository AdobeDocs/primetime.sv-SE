---
title: Översikt över licensanskaffningsprocessen
description: Översikt över licensanskaffningsprocessen
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Översikt över licensförvärvsprocessen{#license-acquisition-process-overview}

Hur du gör det möjligt för ditt program att spela upp innehåll under skydd av Primetime DRM beskrivs i följande avsnitt med hjälp av kodexempel i ActionScript 3 (AS3). Avvikelserna från det här arbetsflödet för inbyggda appar på mobilplattformar presenteras där det är lämpligt. Arbetsflödena för Primetime DRM är dock mycket lika för alla plattformar, så om du förstår AS3-koden blir det ganska enkelt att extrapolera till andra plattformar.

**Licensanskaffningsprocess:**

1. Hämta det skyddade innehållets DRM-metadata.
1. Kontrollera om det finns en licens lokalt:

   * Om licensen är tillgänglig lokalt läser du in licensen och går till steg 6.
   * Om licensen inte är tillgänglig lokalt går du vidare till steg 3.

1. Kontrollera om autentisering krävs:

   * Om autentisering krävs hämtar du inloggningsuppgifterna från användaren och skickar dem till licensservern.
   * Om autentisering inte krävs går du till steg 6.

1. Om registrering av enhetsdomän krävs går du med i enhetsdomänen.
1. Hämta licensen från licensservern om autentisering behövdes och nu är slutförd.
1. Spela upp innehållet.

Om inga fel uppstod och användaren autentiserades för att visa innehållet, skickar Primetime ett `DRMStatusEvent`-objekt och programmet påbörjar uppspelningen. Objektet `DRMStatusEvent` innehåller relaterad licensinformation, som identifierar användarens profil och behörigheter. `DRMStatusEvent` kan till exempel innehålla information om huruvida innehållet kan göras tillgängligt offline, när licensen upphör och så vidare.

Programmet kan använda licensinformationen för att informera användaren om statusen för sin profil. Programmet kan till exempel visa antalet återstående dagar som användaren har för att visa innehållet i ett statusfält. Om användaren tillåts åtkomst offline cachelagras licensen och det krypterade innehållet hämtas till användarens dator. Innehållet är tillgängligt under den tid som anges i licensens cachelagringstid. Egenskapen detail i händelsen innehåller `DRM.voucherObtained`. Programmet bestämmer var innehållet ska lagras lokalt för att kunna vara tillgängligt offline. Du kan även förhandsladda licenser med klassen `DRMManager`.
