---
title: Antal datorer när licenser utfärdas
description: Antal datorer när licenser utfärdas
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Antal datorer när licenser utfärdas{#machine-count-when-issuing-licenses}

Om affärsreglerna kräver att antalet datorer för en användare spåras, måste licensservern eller domänservern lagra de dator-ID som är associerade med användaren. Det mest robusta sättet att spåra dator-ID:n är att lagra värdet som returneras av metoden `MachineId.getBytes()` i en databas. När en ny begäran kommer in kan du jämföra dator-ID:t i begäran med kända dator-ID:n med `MachineId.matches()`.

`MachineId.matches()` utför en jämförelse av ID:n för att avgöra om de representerar samma dator. Jämförelsen är bara praktisk om det finns ett litet antal dator-ID att jämföra med. Om en användare till exempel tillåts fem datorer i sin domän, kan du söka i databasen efter de dator-ID som är kopplade till användarens användarnamn och få en liten uppsättning data att jämföra med.

>[!NOTE]
>
>Den här jämförelsen är inte praktisk för distributioner som tillåter anonym åtkomst. I sådana fall kan `MachineId.getUniqueID()` användas, men detta ID är inte detsamma om användaren öppnar innehåll från både Flash och Adobe AIR®, och kommer inte att överleva om användaren formaterar om hårddisken.

Mer information om `MachineToken.getMachineId()`och `MachineId.matches()` finns i *API-referens för Adobe Access*.
