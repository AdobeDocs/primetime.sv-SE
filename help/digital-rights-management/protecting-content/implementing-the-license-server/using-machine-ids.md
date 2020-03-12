---
seo-title: Använd datoridentifierare
title: Använd datoridentifierare
uuid: 14eee414-62f1-4a9d-84bd-689ca2271d19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Använd datoridentifierare{#use-machine-identifiers}

Alla Adobe Primetime DRM-begäranden (med undantag för begäranden som stöder FMRMS-kompatibilitet) innehåller information om den maskintoken som har utfärdats till klienten under personaliseringen. Datortoken innehåller ett dator-ID, som är en identifierare som har tilldelats under personaliseringen. Du kan använda den här identifieraren för att räkna antalet datorer från vilka en användare har begärt en licens eller anslutit till en domän.

Du kan använda en identifierare på följande sätt:

* Metoden returnerar `getUniqueId()` en sträng som har tilldelats en enhet under personaliseringen. Du kan lagra strängarna i en databas och söka efter identifierare. Den här identifieraren ändras emellertid om användaren formaterar om hårddisken och anpassar den igen. Den här identifieraren har också ett annat värde mellan Adobe AIR och Adobe Flash Player i olika webbläsare på samma dator.
* Om du vill räkna datorer mer korrekt kan du använda `getBytes()` för att lagra hela identifieraren. Om du vill avgöra om datorn har setts tidigare hämtar du alla identifierare för ett användarnamn och anropar `matches()` för att kontrollera om det finns några matchningar. Eftersom metoden måste användas för att jämföra de värden som returneras av `matches()` `MachineId.getBytes`är detta alternativ endast praktiskt när det finns ett litet antal värden att jämföra. till exempel de datorer som är kopplade till en viss användare.

