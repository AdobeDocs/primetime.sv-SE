---
seo-title: Antal datorer när licenser utfärdas
title: Antal datorer när licenser utfärdas
uuid: d57f8b0b-0363-4b26-bd71-76f4abe5b68f
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Antal datorer när licenser utfärdas{#machine-count-when-issuing-licenses}

Om affärsreglerna kräver att antalet datorer för en användare spåras, måste licensservern eller domänservern lagra de dator-ID som är associerade med användaren. Det mest robusta sättet att spåra dator-ID:n är att lagra värdet som returneras av `MachineId.getBytes()` metoden i en databas. När en ny begäran kommer in, jämför du dator-ID:t i begäran med kända dator-ID:n som använder `MachineId.matches()`.

`MachineId.matches()` utför en jämförelse av ID:n för att avgöra om de representerar samma dator. Jämförelsen är bara praktisk om det finns ett litet antal dator-ID att jämföra med. Om en användare till exempel tillåts fem datorer i sin domän, kan du söka i databasen efter de dator-ID som är kopplade till användarens användarnamn och få en liten uppsättning data att jämföra med.

>[!NOTE]
>
>Den här jämförelsen är inte praktisk för distributioner som tillåter anonym åtkomst. I sådana fall `MachineId.getUniqueID()` kan dock detta ID inte användas om användaren öppnar innehåll från både Flash och Adobe AIR® och inte överlever om användaren formaterar om hårddisken.

Mer information om `MachineToken.getMachineId()`och `MachineId.matches()`finns i API-referens för *Adobe Access*.
