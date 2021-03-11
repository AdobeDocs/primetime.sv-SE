---
title: Lagra profiler på ett säkert sätt
description: Lagra profiler på ett säkert sätt
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Säker lagring av profiler{#securely-storing-policies}

Adobe Access SDK är mycket flexibelt när det gäller utveckling av applikationer som ska användas vid paketering av innehåll och framtagning av policyer. När du skapar sådana program kanske du vill tillåta vissa användare att skapa och ändra profiler och begränsa andra användare så att de bara kan tillämpa befintliga profiler på innehållet. Om så är fallet måste du implementera de nödvändiga åtkomstkontrollerna för att skapa användarkonton med olika behörigheter för att skapa principer och för att tillämpa principer på innehållet.

Profiler är inte signerade eller på annat sätt skyddade från ändringar förrän de används i paketeringen. Om du är oroad över användare av dina paketeringsverktyg som ändrar profiler bör du överväga att signera profilerna för att vara säker på att de inte kan ändras.

Mer information om hur du skapar program med SDK finns i *API-referens för Adobe Access*.
