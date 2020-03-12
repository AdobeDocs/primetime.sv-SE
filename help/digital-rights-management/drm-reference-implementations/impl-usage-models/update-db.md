---
seo-title: Uppdatera referensimplementeringsdatabasen
title: Uppdatera referensimplementeringsdatabasen
uuid: 2883045e-ad62-466d-94a2-fc45ded2a4f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uppdatera referensimplementeringsdatabasen{#update-the-reference-implementation-db}

Om du vill styra vilka användningsmodeller som en licens utfärdas till en utsedd användare lägger du till poster i databasen för referensimplementering.

1. Lägg till poster i `Customer` tabellen.

   Tabellen `Customer` innehåller användarnamn och lösenord för att autentisera användare. Det anger också om en användare har en prenumeration (en licens som utfärdas enligt *prenumerationsanvändningsmodellen* ).

1. Ge en användare åtkomst enligt användningsmodellerna Hämta till äga eller Video på begäran.

       Lägg till poster i tabellen &quot;CustomerAuthorization&quot; för att specificera:
   
   * Användningsmodellen
   * Varje innehållssegment som en användare har tillgång till

Mer information om hur du fyller i tabellerna finns i skriptet (som finns på dvd-skivan med Primetime DRM i [!DNL PopulateSampleDB.sql] [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] katalogen).
