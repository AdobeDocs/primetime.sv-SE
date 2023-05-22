---
title: Uppdatera referensimplementeringsdatabasen
description: Uppdatera referensimplementeringsdatabasen
copied-description: true
exl-id: b337bf9c-7add-47b8-9576-db7fa067c51d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Uppdatera referensimplementeringsdatabasen{#update-the-reference-implementation-db}

Om du vill styra vilka användningsmodeller som en licens utfärdas till en utsedd användare lägger du till poster i databasen för referensimplementering.

1. Lägg till poster i `Customer` tabell.

   The `Customer` tabellen innehåller användarnamn och lösenord för att autentisera användare. Det anger också om en användare har en prenumeration (en licens som utfärdas under *Prenumeration* användningsmodell).

1. Ge en användare åtkomst enligt användningsmodellerna Hämta till äga eller Video på begäran.

       Lägg till poster i tabellen &quot;CustomerAuthorization&quot; för att specificera:
   
   * Användningsmodellen
   * Varje innehållssegment som en användare har tillgång till

Mer information om hur du fyller i varje tabell finns i [!DNL PopulateSampleDB.sql] skript (finns på din Primetime DRM DVD i [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] katalog).
