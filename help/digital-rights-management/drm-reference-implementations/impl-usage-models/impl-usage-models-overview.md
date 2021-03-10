---
title: Översikt
description: Översikt
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Översikt{#overview}

Referensimplementeringen innehåller ett demonstrationsläge som visar hur du implementerar olika användningsmodeller för ett segment med paketerat innehåll. Demoläget innehåller affärslogik för dessa användningsmodeller:

* **DTO (Download To-Own)**  - Användare kan hämta innehållet online eller offline och får en permanent licens för innehållet.
* **Uthyrning/video-on-demand (VOD)**  - Det tillgängliga innehållet levereras med tidsbaserade begränsningar. Användare kan till exempel spela upp innehåll under en 30-dagarsperiod. När uppspelningen börjar har användaren upp till 48 timmar på sig att titta klart på innehållet. Innehållet måste visas inom 30 dagar.
* **Prenumeration (all-du-can-eat)**  - Vissa tjänster erbjuder betalda prenumerationer som ger användarna obegränsad tillgång till ett stort innehållsbibliotek så länge de fortsätter att betala en månadsavgift. Licensservern utfärdar en unik licens för varje innehållssegment och utfärdar också en rotlicens som upphör i slutet av prenumerationsperioden. Varje månad måste rotlicensen också förnyas när användare förnyar sin prenumeration.

   >[!NOTE]
   >
   >För de föregående användningsmodellerna måste användarna ange sina inloggningsuppgifter när de har skaffat en licens, så att servern kan verifiera att användarna har ett uthyrningskonto.

* **Annonsfinansierad**  - Innehållet genereras genom att annonsering inkluderas som en del av upplevelsen. Med den här modellen kan innehåll distribueras och kräver ingen användarautentisering.

I demoläge för användningsmodell styr serverns affärslogik attributen för genererade licenser. Vid paketeringen behöver DRM-principen bara ange om autentisering krävs eller inte.

Om du vill aktivera alla fyra användningsmodellerna behöver du bara inkludera två DRM-principer:

* En DRM-princip som tillåter anonym åtkomst för den annonsfinansierade modellen
* En DRM-princip som kräver autentisering av användarnamn/lösenord för de tre andra användningsmodellerna.

När en användare begär en licens kan ett klientprogram avgöra om användaren ska tillfrågas om autentisering baserat på autentiseringsinformationen i DRM-principerna.
