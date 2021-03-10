---
title: Uppdatera referensimplementeringsdatabasen
description: Uppdatera referensimplementeringsdatabasen
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Uppdatera referensimplementeringsdatabasen{#update-the-reference-implementation-db}

Om du vill styra vilka användningsmodeller som en licens utfärdas till en utsedd användare lägger du till poster i databasen för referensimplementering.

1. Lägg till poster i tabellen `Customer`.

   Tabellen `Customer` innehåller användarnamn och lösenord för att autentisera användare. Det anger också om en användare har en prenumeration (en licens som utfärdas enligt *prenumerationsmodellen*).

1. Ge en användare åtkomst enligt användningsmodellerna Hämta till äga eller Video på begäran.

       Lägg till poster i tabellen &quot;CustomerAuthorization&quot; för att specificera:
   
   * Användningsmodellen
   * Varje innehållssegment som en användare har tillgång till

Mer information om hur du fyller i varje tabell finns i [!DNL PopulateSampleDB.sql]-skriptet (som finns på din Primetime DRM DVD i katalogen [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/]).
