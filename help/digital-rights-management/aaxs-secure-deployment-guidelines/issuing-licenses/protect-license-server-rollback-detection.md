---
title: Återställningsigenkänning
description: Återställningsigenkänning
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Återställningsidentifiering {#rollback-detection}

Om din implementering av Adobe Access använder affärsregler som kräver att klienten behåller läget (till exempel intervallet för uppspelningsfönstret), rekommenderar Adobe att servern håller reda på återställningsräknaren och använder AIR eller SWF som tillåter listning.

Återställningsräknaren skickas till servern i de flesta begäranden från klienten. Om återställningsräknaren inte behövs för implementeringen av Adobe Access kan den ignoreras. I annat fall rekommenderar Adobe att servern lagrar det slumpmässiga dator-ID som erhållits med `MachineToken.getMachineId().getUniqueId()` och det aktuella räknarvärdet i en databas. Mer information om hur du ökar och spårar återställningsräknaren finns i ClientState i *API-referens för Adobe Access* och *Återställningsidentifiering* i *Använda Adobe Access SDK för att skydda innehåll*.
