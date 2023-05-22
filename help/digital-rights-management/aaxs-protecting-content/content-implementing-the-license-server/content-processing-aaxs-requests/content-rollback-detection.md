---
title: Återställningsigenkänning
description: Återställningsigenkänning
copied-description: true
exl-id: 525ae64e-1ade-4661-8403-ee4e42181358
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Återställningsigenkänning{#rollback-detection}

För återställningsidentifiering kräver vissa användningsregler att klienten upprätthåller tillståndsinformation för att rättigheterna ska kunna verkställas. För att t.ex. framtvinga regler för användning av uppspelningsfönstret lagrar klienten det datum och den tidpunkt då användaren först började visa innehållet. Den här händelsen startar uppspelningsfönstrets start. För att på ett säkert sätt framtvinga uppspelningsfönstret måste servern se till att användaren inte säkerhetskopierar och återställer klientens tillstånd för att ta bort uppspelningsfönstrets starttid som lagrats på klienten. Servern gör detta genom att spåra värdet för klientens återställningsräknare. Servern hämtar räknarens värde för varje begäran genom att anropa `RequestMessageBase.getClientState()` för att få `ClientState` objekt, anropa `ClientState.getCounter()` för att hämta det aktuella värdet för klienttillståndsräknaren. Servern bör lagra värdet för varje klient (använd `MachineId.getUniqueId()` för att identifiera klienten som är associerad med värdet för återställningsräknaren) och sedan anropa `ClientState.incrementCounter()` för att öka räknarvärdet med ett. Om servern upptäcker att räknarvärdet är mindre än det senaste värdet som servern ser kan klienttillståndet ha återställts. Mer information om identifiering av otillåtna klienttillstånd finns i `ClientState` API-referensdokumentation.
