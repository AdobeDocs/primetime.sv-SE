---
seo-title: Lagra profiler på ett säkert sätt
title: Lagra profiler på ett säkert sätt
uuid: b1ac236f-6637-46d4-8405-a819d6093314
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Lagra profiler på ett säkert sätt{#securely-storing-policies}

Adobe Access SDK är mycket flexibelt när det gäller utveckling av applikationer som ska användas vid paketering av innehåll och framtagning av policyer. När du skapar sådana program kanske du vill tillåta vissa användare att skapa och ändra profiler och begränsa andra användare så att de bara kan tillämpa befintliga profiler på innehållet. Om så är fallet måste du implementera de nödvändiga åtkomstkontrollerna för att skapa användarkonton med olika behörigheter för att skapa principer och för att tillämpa principer på innehållet.

Profiler är inte signerade eller på annat sätt skyddade från ändringar förrän de används i paketeringen. Om du är oroad över användare av dina paketeringsverktyg som ändrar profiler bör du överväga att signera profilerna för att vara säker på att de inte kan ändras.

Mer information om hur du skapar program med SDK finns i API-referens *för* Adobe Access.
