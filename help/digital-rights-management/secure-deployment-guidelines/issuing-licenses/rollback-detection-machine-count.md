---
description: Om affärsreglerna kräver att antalet datorer för en användare spåras, måste licensservern eller domänservern lagra de dator-ID som är associerade med användaren.
title: Antal datorer när licenser utfärdas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Antal datorer när licenser utfärdas {#machine-count-when-issuing-licenses}

Om affärsreglerna kräver att antalet datorer för en användare spåras, måste licensservern eller domänservern lagra de dator-ID som är associerade med användaren.

Det mest robusta sättet att spåra dator-ID:n är att lagra värdet som returneras av metoden [MachineId.getBytes()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getBytes()) i en databas. När en ny begäran tas emot kan du jämföra dator-ID:t i begäran med kända dator-ID:n med [MachineId.match()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)).

[MachineId.match()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#matches(com.adobe.flashaccess.sdk.cert.MachineId)) utför en jämförelse av ID:n för att avgöra om ID:n representerar samma dator. Jämförelsen är bara praktisk om det finns ett litet antal dator-ID. Om användare till exempel tillåts fem datorer i sin domän, kan du söka i databasen efter de dator-ID som är kopplade till användarens användarnamn och få en liten uppsättning data för jämförelse.

Den här jämförelsen är inte praktisk för distributioner som tillåter anonym åtkomst. I det här fallet kan [MachineId.getUniqueID()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()) användas. Detta ID kan dock inte vara samma om användaren öppnar innehåll från Flash och Adobe AIR®.

>[!NOTE]
>
>ID:t fungerar inte om användaren formaterar om hårddisken.