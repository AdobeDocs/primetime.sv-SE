---
seo-title: Återställningsigenkänning
title: Återställningsigenkänning
uuid: cc554194-2848-4104-85eb-f697a86c72f2
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Återställningsigenkänning{#rollback-detection}

För återställningsidentifiering kräver vissa användningsregler att klienten upprätthåller tillståndsinformation för att rättigheterna ska kunna verkställas. För att t.ex. framtvinga regler för användning av uppspelningsfönstret lagrar klienten det datum och den tidpunkt då användaren först började visa innehållet. Den här händelsen startar uppspelningsfönstrets start. För att på ett säkert sätt framtvinga uppspelningsfönstret måste servern se till att användaren inte säkerhetskopierar och återställer klientens tillstånd för att ta bort uppspelningsfönstrets starttid som lagrats på klienten. Servern gör detta genom att spåra värdet för klientens återställningsräknare. För varje begäran hämtar servern räknarens värde genom att anropa `RequestMessageBase.getClientState()` för att hämta `ClientState` objektet och sedan anropa `ClientState.getCounter()` för att erhålla det aktuella värdet för klienttillståndsräknaren. Servern bör lagra det här värdet för varje klient (använd `MachineId.getUniqueId()` för att identifiera klienten som är associerad med återställningsräknarens värde) och sedan anropa `ClientState.incrementCounter()` för att öka räknarvärdet med ett. Om servern upptäcker att räknarvärdet är mindre än det senaste värdet som servern ser kan klienttillståndet ha återställts. Mer information om identifiering av otillåtna klienttillstånd finns i API-referensdokumentationen `ClientState` .
