---
seo-title: Återställningsigenkänning
title: Återställningsigenkänning
uuid: fc80c98f-7ee5-414b-87fe-0dbb8d4f6019
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Återställningsigenkänning{#rollback-detection}

Om din implementering av Adobe Access använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR- eller SWF-tillåtelse.

Återställningsräknaren skickas till servern i de flesta begäranden från klienten. Om din implementering av Adobe Access inte kräver återställningsräknaren kan den ignoreras. I annat fall rekommenderar Adobe att servern lagrar det slumpmässiga dator-ID som erhållits med `MachineToken.getMachineId().getUniqueId()`och det aktuella räkningsvärdet i en databas. Mer information om hur du ökar och spårar återställningsräknaren finns i ClientState i *Adobe Access API Reference* and *Rollback detection* i *Använda Adobe Access SDK för att skydda innehåll*.
