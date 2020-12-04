---
seo-title: Använda datoridentifierare
title: Använda datoridentifierare
uuid: 2832c158-fade-4bbf-ae89-f95ce9dfc369
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Använda maskinidentifierare{#using-machine-identifiers}

Alla Adobe Access-begäranden (med undantag för begäranden som stöder FMRMS-kompatibilitet) innehåller information om den maskintoken som utfärdas till klienten under personaliseringen. Datortoken innehåller ett dator-ID, en identifierare som tilldelats under personaliseringen. Använd den här identifieraren för att räkna antalet datorer från vilka en användare har begärt en licens eller anslutit till en domän.

Det finns två sätt att använda identifieraren på. Metoden `getUniqueId()` returnerar en sträng som tilldelats enheten under individualisering. Du kan lagra strängarna i en databas och söka efter identifierare. Den här identifieraren ändras emellertid om användaren formaterar om hårddisken och anpassar den igen. Den här identifieraren kommer också att ha ett annat värde mellan Adobe® AIR® och Adobe® Flash® Player i olika webbläsare på samma dator.

Om du vill räkna datorer mer korrekt kan du använda `getBytes()` för att lagra hela identifieraren. Om du vill avgöra om datorn har setts tidigare hämtar du alla identifierare för ett användarnamn och anropar `matches()` för att kontrollera om det finns några matchningar. Eftersom metoden `matches()` måste användas för att jämföra de värden som returneras av `MachineId.getBytes` är det här alternativet bara praktiskt när det finns ett litet antal värden att jämföra (till exempel de datorer som är kopplade till en viss användare).
