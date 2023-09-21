---
title: Använda datoridentifierare
description: Använda datoridentifierare
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Använda datoridentifierare{#using-machine-identifiers}

Alla Adobe Access-begäranden (med undantag för begäranden som stöder FMRMS-kompatibilitet) innehåller information om den maskintoken som utfärdas till klienten under personaliseringen. Datortoken innehåller ett dator-ID, en identifierare som tilldelats under personaliseringen. Använd den här identifieraren för att räkna antalet datorer från vilka en användare har begärt en licens eller anslutit till en domän.

Det finns två sätt att använda identifieraren på. The `getUniqueId()` returnerar en sträng som tilldelats enheten under personaliseringen. Du kan lagra strängarna i en databas och söka efter identifierare. Den här identifieraren ändras emellertid om användaren formaterar om hårddisken och anpassar den igen. Den här identifieraren har också ett annat värde mellan Adobe® AIR® och Adobe® Flash® Player i olika webbläsare på samma dator.

Om du vill räkna datorer mer korrekt kan du använda `getBytes()` för att lagra hela identifieraren. Hämta alla identifierare för ett användarnamn och anrop för att avgöra om datorn har setts tidigare `matches()` för att kontrollera om det finns någon matchning. På grund av `matches()` -metoden måste användas för att jämföra de värden som returneras av `MachineId.getBytes`är det här alternativet bara praktiskt när det finns ett litet antal värden att jämföra (till exempel datorer som är kopplade till en viss användare).
