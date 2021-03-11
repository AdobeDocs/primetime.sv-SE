---
title: Återställningsigenkänning
description: Återställningsigenkänning
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Återställningsidentifiering{#rollback-detection}

För återställningsidentifiering kräver vissa användningsregler att klienten upprätthåller tillståndsinformation för att rättigheterna ska kunna verkställas. För att t.ex. framtvinga regler för användning av uppspelningsfönstret lagrar klienten det datum och den tidpunkt då användaren först började visa innehållet. Den här händelsen startar uppspelningsfönstrets start. För att på ett säkert sätt framtvinga uppspelningsfönstret måste servern se till att användaren inte säkerhetskopierar och återställer klientens tillstånd för att ta bort uppspelningsfönstrets starttid som lagrats på klienten. Servern gör detta genom att spåra värdet för klientens återställningsräknare. Servern hämtar räknarens värde för varje begäran genom att anropa `RequestMessageBase.getClientState()` för att hämta `ClientState`-objektet och sedan anropa `ClientState.getCounter()` för att få fram det aktuella värdet för klienttillståndsräknaren. Servern bör lagra det här värdet för varje klient (använd `MachineId.getUniqueId()` för att identifiera klienten som är associerad med återställningsräknarvärdet) och anropa sedan `ClientState.incrementCounter()` för att öka räknarvärdet med ett. Om servern upptäcker att räknarvärdet är mindre än det senaste värdet som servern ser kan klienttillståndet ha återställts. Mer information om identifiering av manipulering av klienttillstånd finns i `ClientState` API-referensdokumentationen.
