---
title: Antal datorer när licenser utfärdas
description: Antal datorer när licenser utfärdas
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# Antal datorer när licenser utfärdas{#machine-count-when-issuing-licenses}

Om affärsreglerna kräver att antalet datorer för en användare spåras, måste licensservern eller domänservern lagra de dator-ID som är associerade med användaren. Det mest robusta sättet att spåra dator-ID:n är att lagra värdet som returneras av `MachineId.getBytes()` i en databas. När en ny begäran kommer in, jämför du dator-ID:t i begäran med kända dator-ID:n som använder `MachineId.matches()`.

`MachineId.matches()` utför en jämförelse av ID:n för att avgöra om de representerar samma dator. Jämförelsen är bara praktisk om det finns ett litet antal dator-ID att jämföra med. Om en användare till exempel tillåts fem datorer i sin domän, kan du söka i databasen efter de dator-ID som är kopplade till användarens användarnamn och få en liten uppsättning data att jämföra med.

>[!NOTE]
>
>Den här jämförelsen är inte praktisk för distributioner som tillåter anonym åtkomst. I sådana fall `MachineId.getUniqueID()` Detta ID kan dock inte användas om användaren öppnar innehåll från både Flash och Adobe AIR®, och kommer inte att överleva om användaren formaterar om hårddisken.

Mer information om `MachineToken.getMachineId()`och `MachineId.matches()`, se *API-referens för Adobe Access*.
